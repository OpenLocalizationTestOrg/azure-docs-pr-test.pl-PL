---
title: "aaaFundamentals Zarządzanie tożsamościami Azure | Dokumentacja firmy Microsoft"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Podstawowe informacje na temat zarządzania tożsamość platformy Azure
Jako coraz więcej zasobów cyfrowych firmy na żywo poza siecią firmową hello, w chmurze hello i na urządzeniach, staje się bardzo oparte na chmurze tożsamościami i dostępem rozwiązania do zarządzania to konieczne. Tożsamości w chmurze są teraz hello najlepsze sposób toomaintain kontroli over i widoczność, jak i kiedy użytkownicy uzyskują dostęp do danych i aplikacji firmy.

Microsoft ma zostały zabezpieczanie tożsamości opartej na chmurze dla za pośrednictwem dekadę, a teraz z [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), tych samych systemów ochrony są dostępne tooyou. Z usługą Azure AD Administratorzy przedsiębiorstwa można łatwo zapewnienia accountability użytkownika i administratora z lepszych zabezpieczeń i zarządzania niż kiedykolwiek wcześniej.

Azure AD Premium jest oparta na chmurze tożsamościami i dostępem rozwiązaniem do zarządzania z funkcji ochrony zaawansowane umożliwiającą jedną tożsamość bezpieczne dla wszystkich aplikacji, ochrona tożsamości (przez hello [Microsoft analizy zabezpieczeń wykres](https://www.microsoft.com/en-us/security/intelligence)), a Privileged Identity Management. Nie po prostu inną monitorowania lub narzędzia do raportowania Azure AD Premium można chronić tożsamości użytkownika w czasie rzeczywistym i włączyć możesz toocreate ryzyka, adaptacyjną dostęp zasady tooprotect danych organizacji.

Obejrzyj ten krótki film, aby szybko zapoznać zarządzania tożsamościami w usłudze Azure AD i ochrony:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft nie tylko udostępnia tożsamości, która przyjmuje wszędzie, ale także zestaw narzędzi tooautomate, zabezpieczania oraz zarządzania nimi IT w organizacji. Nawet po pojawienie się hello chmury obliczeniowej, jest nadal popytu toomanage i kontrolować IT zadań, takich jak pomoc techniczna wywołuje tooreset hasła użytkownika użytkownik grupy zarządzania i żądania aplikacji. Komplikując dalsze czynności, pracownicy są teraz dostarczają toowork ich urządzeń osobistych i przy użyciu aplikacji SaaS łatwo dostępne. Dzięki temu zachowując kontrolę nad ich aplikacji firmowych centrów danych i chmurze publicznej platformy istotne wyzwanie.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Połączenie lokalnej usługi Active Directory z usługą Azure AD i Office 365
Organizacje, które zostały wprowadzone dużych inwestycji w lokalnej usłudze Active Directory można rozszerzyć te chmury toohello inwestycji dzięki integracji z usługą Azure AD do ich w lokalnych katalogach [hybrydowe Zarządzanie tożsamościami](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Dzięki temu użytkownicy bardziej wydajnej pracy, zapewniając wspólną tożsamość do uzyskiwania dostępu do zasobów, niezależnie od lokalizacji. Użytkowników i organizacji można następnie użyj funkcji logowania jednokrotnego (SSO) tooaccess zarówno zasobów lokalnych i usług, takich jak Office 365 w chmurze.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) jest jedynym narzędziem hello należy integracji hello tooget gotowe. Azure AD Connect zapewnia możliwości toosupport Twojego synchronizacji tożsamości musi i zastępuje starsze wersje narzędzi do integracji tożsamości, takie jak DirSync i Azure AD Sync. Z programem Azure AD Connect za pośrednictwem włączono zarządzanie tożsamościami i synchronizacji między lokalnymi i usługą Azure AD:

- Synchronizacja — ten składnik odpowiada za tworzenie użytkowników, grup i innych obiektów. Jest również odpowiedzialny za zapewnienie, że informacje o tożsamości dla lokalnych użytkowników i grup jest zgodne z hello chmury. Zapisywania zwrotnego haseł można także synchronizację katalogów lokalnych tookeep włączone, gdy użytkownik zaktualizuje hasła w usłudze Azure AD.
- Usługi AD FS - Federacja znajduje się funkcja opcjonalna udostępniane przez usługi Azure AD Connect, które mogą być używane tooconfigure w środowisku hybrydowym przy użyciu lokalnej infrastruktury usług AD FS. Federacyjna służy organizacje tooaddress złożone wdrożenia, takich jak logowanie jednokrotne, wymuszanie AD zasad logowania, a karta inteligentna lub innej usługi MFA.
- Monitorowanie kondycji — [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) można zapewnia zaawansowane monitorowanie i podaj centralnej lokalizacji w hello Azure tooview portalu tego działania.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Zwiększyć wydajność i zmniejszyć koszty pomocy technicznej z samoobsługi i jednego znaku w ramach

Pracownicy są bardziej wydajni, jeśli mają jeden tooremember nazwy użytkownika i hasła i spójne środowisko z każdego urządzenia. One również zaoszczędzić czas, kiedy można wykonać samoobsługi zadania, takie jak [zresetować zapomniane hasło](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) lub żądania dostępu tooan aplikacji bez oczekiwania na powitania pomocy technicznej o pomoc.

Usługi Azure AD [rozszerza w lokalnej usłudze Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) w chmurze hello włączenie toouse użytkowników swoje konta organizacyjne głównej zarówno urządzeń przyłączonych do domeny, zasobów firmy i wszystkie hello sieci web i aplikacji SaaS one należy toouse tooget swoich zadań gotowe. Ponadto toonot o tooremember wiele zestawów nazwy użytkownika i hasła, dostęp do aplikacji użytkowników można również można automatycznie udostępniane (lub usuwane) na podstawie ich członkostwa w grupach organizacji i ich stan jako pracownika. Można kontrolować tego dostępu dla aplikacji w galerii lub własnych aplikacji lokalnych, został opracowany i opublikowanych za pośrednictwem hello [serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Zarządzanie i sterowanie dostęp do zasobów toocorporate
Pomocy firmy Microsoft tożsamościami i dostępem zarządzania rozwiązań IT ochronę tooapplications dostępu i zasobów na powitania firmowym centrum danych i w chmurze hello, takich jak włączenie dodatkowe poziomy weryfikacji [uwierzytelnianie wieloskładnikowe](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) i [zasady dostępu warunkowego](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Monitorowania podejrzanych działań przez zaawansowane zabezpieczenia raportowania, inspekcji i alerty, pomaga ograniczyć potencjalne problemy.

Zasady dostępu warunkowego w usłudze Azure AD Premium, zapewniają hello administratora przedsiębiorstwa, hello możliwości toocreate opartych na zasadach reguł dostępu dla dowolnego Azure połączone AD aplikacji (aplikacji SaaS, niestandardowe aplikacje działające w aplikacji sieci web hello chmurze lub lokalnie). Usługi Azure AD ocenia te zasady w czasie rzeczywistym i wymusza je zawsze, gdy użytkownik próbuje tooaccess aplikacji. Tożsamość platformy Azure, zasady ochrony włączyć działania tooautomatically Jeśli zostało wykryte podejrzane działania. Te operacje mogą zawierać blokowanie dostępu toousers o wysokim ryzyku, wymuszając uwierzytelnianie wieloskładnikowe i resetowanie haseł użytkowników, jeśli wygląda poświadczenia zostały naruszone.


## <a name="azure-active-directory-privileged-identity-management"></a>Zarządzanie uprzywilejowanymi tożsamościami usługi Azure Active Directory

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started), dołączonego hello Azure Active Directory Premium P2 oferty, pozwala toodiscover ograniczyć i monitorować konta z uprawnieniami administracyjnymi i ich tooresources dostępu w usłudze Azure Active Directory i innych Usługi online firmy Microsoft. Pomaga również administrowania hello dokładny okres czasu potrzebnego na żądanie dostępu administracyjnego.

Zarządzanie tożsamościami uprzywilejowanymi można wymusić uprawnień administratora na żądanie tak, aby administratorzy mogą żądać wieloskładnikowego uwierzytelniony, tymczasowy podniesienie swoje uprawnienia dla wstępnie skonfigurowane okresów przed ich kont zwracać tooa normalne Stan użytkownika.

## <a name="benefits-of-azure-identity"></a>Zalety tożsamość platformy Azure

Tożsamość platformy Azure management można:

-   Tworzenie i zarządzanie nimi jednej tożsamości dla każdego użytkownika w całym przedsiębiorstwie, synchronizacja użytkowników, grup i urządzeń z [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Podaj dostępu rejestracji jednokrotnej tooyour aplikacji, w tym tysięcy wstępnie zintegrowanych aplikacji SaaS lub zapewniania bezpiecznego dostępu zdalnego tooon lokalnych aplikacji SaaS przy użyciu hello [serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Włącz zabezpieczenie dostępu do aplikacji przez wymuszenie opartych na regułach [uwierzytelnianie wieloskładnikowe](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) dla lokalnych i w chmurze aplikacji.

-   Zwiększenie produktywności użytkowników z [samoobsługowego resetowania hasła](https://docs.microsoft.com/azure/active-directory/active-directory-passwords)i grupy, jak i aplikacji przy użyciu hello żądań dostępu [MyApps portal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Zalety hello [wysokiej dostępności i niezawodności](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) na całym świecie, klasy przedsiębiorstwa, oparte na chmurze tożsamościami i dostępem rozwiązania do zarządzania.

## <a name="next-steps"></a>Następne kroki
[Więcej informacji o rozwiązaniach tożsamość platformy Azure](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)