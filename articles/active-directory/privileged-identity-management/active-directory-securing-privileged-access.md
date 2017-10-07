---
title: "aaaSecuring uprzywilejowanego dostępu w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Temat opisujący hello zbliża się do zabezpieczania uprzywilejowanego dostępu na platformie Azure, Azure Active Directory i usług Microsoft Online Services."
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
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD
Zabezpieczanie uprzywilejowanego dostępu jest pierwszym krokiem krytyczne toohelp ochronę zasobów biznesowych w organizacji modern. Uprzywilejowane konta są kontami, które Administruj i Zarządzaj systemów informatycznych. Osoby atakujące przez docelowe danych organizacji tych kont toogain dostępu tooan i systemów. toosecure uprzywilejowany dostęp, należy odizolowanie kont hello i systemów ryzyko hello jest udostępniany tooa złośliwy użytkownik.

Więcej użytkowników coraz tooget uprzywilejowany dostęp za pośrednictwem usługi w chmurze. Może to obejmować Administratorzy globalni dla usługi Office 365, Administratorzy subskrypcji platformy Azure i użytkowników, którzy mają dostęp administracyjny na maszynach wirtualnych lub w aplikacji SaaS.

Firma Microsoft zaleca wykonanie tego planu [zabezpieczanie uprzywilejowanego dostępu](https://technet.microsoft.com/library/mt631194.aspx).

Dla klientów korzystających z usługi Azure Active Directory, usługi Office 365 lub innych usług firmy Microsoft i aplikacji czy konta użytkowników są zarządzane i uwierzytelniony przez usługę Active Directory lub w usłudze Azure Active Directory stosuje się te zasady. Witaj poniższe sekcje zawierają więcej informacji na zabezpieczanie uprzywilejowanego dostępu toosupport funkcje usługi Azure AD.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
tooincrease hello zabezpieczeń administratora uwierzytelniania, należy włączyć weryfikację dwuetapową przed udzieleniem im uprawnienia. Weryfikacja dwuetapowa jest metodę sprawdzania, kto, które są wymagane jest użycie hello więcej niż tylko nazwę użytkownika i hasło. Zapewnia drugą warstwę logowania toouser zabezpieczeń i transakcji.

Usługa Azure Multi-Factor Authentication (MFA) jest rozwiązania weryfikacji dwuetapowej firmy Microsoft, która pomaga w zabezpieczaniu dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pośrednictwem szereg opcji weryfikacji łatwy w tym:

- połączenia telefoniczne
- Wiadomości SMS
- powiadomienia z aplikacji mobilnej
- kodów weryfikacyjnych aplikacji mobilnej
- Tokeny OATH innej firmy

Omówienie działania usługi Azure Multi-Factor Authentication Zobacz powitania po wideo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Aby uzyskać więcej informacji, zobacz [MFA dla usługi Office 365 i uwierzytelniania Wieloskładnikowego na platformie Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Uprawnienia powiązane z czasu
W niektórych organizacjach może się okazać mają zbyt wielu użytkownikom wysoko uprzywilejowane ról. Użytkownik może zostały dodane toohello rolę dla danego działania, takie jak toosign dla usługi, ale nie był używany często później tych uprawnień.

czas ekspozycji hello toolower uprawnień i zwiększyć Twojej wgląd w ich użycia, biorąc na swoje uprawnienia "just in time" tooonly użytkowników limit (JIT), jeśli potrzebna jest tooperform zadania. W przypadku usługi Azure Active Directory i usług Online firmy Microsoft, można użyć [Azure AD Privileged Identity zarządzania (PIM)](http://aka.ms/AzurePIM).

![Pulpit nawigacyjny usługi PIM][2]

## <a name="attack-detection"></a>Wykrywanie ataków
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji. Oparte na zdarzenia o podwyższonym ryzyku, Identity Protection oblicza poziom ryzyka użytkownika, dla każdego użytkownika, co pozwala chronić tooautomatically zasady oparte na ryzyko tooconfigure hello tożsamości organizacji. Te zasady, oraz innych mechanizmów kontroli dostępu warunkowego zapewniane przez usługę Azure Active Directory i EMS, można automatycznie Blokuj użytkownika hello lub udostępniania sugestii, obejmujące resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.

![Usługa Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Dostęp warunkowy
Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków przez użytkownika podczas uwierzytelniania użytkownika, przed zezwoleniem na dostęp do aplikacji tooan. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji.

![Ustawienie zasad dostępu warunkowego za pomocą usługi MFA][4]

## <a name="related-articles"></a>Pokrewne artykuły:
* Włącz [uwierzytelnianie wieloskładnikowe platformy Azure](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Włącz [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Włącz [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Włącz [kontroli dostępu warunkowego](../active-directory-conditional-access.md)

Aby uzyskać więcej informacji na tworzeniu planu zabezpieczeń pełną sekcji hello "obowiązki klienta i plan" hello [Microsoft Cloud Security dla architektów Enterprise](http://aka.ms/securecustomer) dokumentu. Aby uzyskać więcej informacji na angażowaniu tooassist usług firmy Microsoft za pomocą dowolnego z tych tematów, skontaktuj się z przedstawicielem firmy Microsoft lub odwiedź nasze [strony rozwiązania bezpieczeństwa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
