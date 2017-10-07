---
title: "aaaVulnerabilities wykryta przez usługę Azure Active Directory Identity Protection | Dokumentacja firmy Microsoft"
description: "Przegląd luk w zabezpieczeniach hello wykrywanych przez usługę Azure Active Directory Identity Protection."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Luk w zabezpieczeniach wykrywanych przez usługę Azure Active Directory Identity Protection
Luki w zabezpieczeniach występują słabe strony w danym środowisku, które może być wykorzystane przez atakującego. Zaleca się rozwiązać te luki w zabezpieczeniach tooimprove hello stan zabezpieczeń organizacji i uniemożliwić osobom atakującym ich wykorzystania.


![luki w zabezpieczeniach](./media/active-directory-identityprotection-vulnerabilities/101.png "luk w zabezpieczeniach")



Hello następujące sekcje zawierają omówienie luk w zabezpieczeniach hello zgłoszone przez ochronę tożsamości.

## <a name="multi-factor-authentication-registration-not-configured"></a>Rejestracja usługi Multi-Factor authentication nie jest skonfigurowany
Ta luka w zabezpieczeniach pomaga kontrolować hello wdrożenia usługi Azure Multi-Factor Authentication w organizacji. 

Usługa Azure Multi-Factor authentication udostępnia drugą warstwę zabezpieczeń toouser uwierzytelniania. Ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji łatwe — połączenie telefoniczne, wiadomość tekstowa lub aplikacji mobilnej weryfikacji lub powiadamiania o kod i 3rd strona tokenów OATH.

Firma Microsoft zaleca wymusić uwierzytelnianie wieloskładnikowe Azure logowania użytkownika. Uwierzytelnianie wieloskładnikowe odgrywa kluczową rolę w zasadach dostępu warunkowego opartego na ryzyko dostępne za pośrednictwem Identity Protection.

Aby uzyskać więcej informacji, zobacz [co to jest uwierzytelnianie wieloskładnikowe Azure?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Aplikacje w chmurze niezarządzane
Ta luka w zabezpieczeniach pomaga zidentyfikować aplikacje w chmurze niezarządzane w Twojej organizacji.

W nowoczesnych przedsiębiorstwa działów IT są często zna wszystkie aplikacje chmury hello korzystania przez użytkowników w organizacji toodo służbowym. Jest łatwy toosee Dlaczego Administratorzy byłyby danych toocorporate nieautoryzowanym dostępem, wycieku danych oraz inne zagrożenia dla bezpieczeństwa. 

Firma Microsoft zaleca organizacji do wdrożenia aplikacji w chmurze niezarządzane toodiscover Cloud App Discovery i toomanage te aplikacje przy użyciu usługi Azure Active Directory.

Aby uzyskać więcej informacji, zobacz [znajdowania aplikacji w chmurze niezarządzane z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Alerty zabezpieczeń ze Zarządzanie tożsamościami uprzywilejowanymi
Ta luka w zabezpieczeniach pomaga wykrywać oraz rozwiązywanie alertów dotyczących tożsamości uprzywilejowanych w Twojej organizacji.  

toocarry użytkowników tooenable operacje uprzywilejowane, organizacje muszą także tymczasowych lub trwałych uprzywilejowanego dostępu w usłudze Azure AD, użytkownicy toogrant zasobów platformy Azure lub usługi Office 365 lub innych aplikacji SaaS. Każdy z tych użytkownicy o odpowiednich uprawnieniach zwiększa hello ataku Twojej organizacji. Tę lukę w zabezpieczeniach pomaga zidentyfikować użytkowników z dostępem uprzywilejowanym zbędne i podjąć odpowiednie działania tooreduce lub wyeliminowanie hello ryzyka, które stanowią one. 

Zaleca się, że Twoja organizacja korzysta z usługi Azure AD Privileged Identity Management toomanage, kontroli i monitor uprzywilejowany tożsamości i ich tooresources dostępu w usłudze Azure AD, jak również innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.

Aby uzyskać więcej informacji, zobacz [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Zobacz też
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md)

