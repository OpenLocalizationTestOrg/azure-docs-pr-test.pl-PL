---
title: "tooIntegrate aaaHow w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Toobenefits przewodnik, programu i zasoby do integracji z usługą Azure Active Directory."
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Integracja z usługą Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Usługa Azure Active Directory udostępnia organizacjom korporacyjnej Zarządzanie tożsamościami dla aplikacji w chmurze.  Integracja z usługą Azure AD zwiększa udoskonalone środowisko logowania użytkowników i aplikacja jest zgodna z tooIT zasad.

## <a name="how-toointegrate"></a>Jak tooIntegrate
Istnieje kilka metod dla Twojego toointegrate aplikacji z usługą Azure AD.  Skorzystaj z jako wiele lub kilka z tych scenariuszy, ponieważ jest odpowiedni dla twojej aplikacji.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Obsługa usługi Azure AD jako tooSign sposób w tooYour aplikacji
**Zmniejsz logowania tarcia i zmniejszyć koszty pomocy technicznej.** Przy użyciu usługi Azure AD toosign tooyour aplikacji, użytkownicy nie mają jednego więcej tooremember nazwy i hasła.  Dewelopera możesz mieć jeden mniej toostore hasła i ochrony.  Nie ma resetowanie haseł toohandle zapomnienia hasła może być znaczne oszczędności, samodzielnie.  Usługi Azure AD uprawnień logowania dla niektórych Witaj świecie najbardziej popularnych aplikacji w chmurze, w tym usługi Office 365 i Microsoft Azure.  Setki milionów użytkowników z milionów organizacji, prawdopodobnie użytkownika jest już zalogowany tooAzure AD.  Dowiedz się więcej o [dodanie obsługi usługi Azure AD w celu logowania się](active-directory-authentication-scenarios.md).

**Uproszczenie logowania się aplikacji.**  Podczas tworzenia konta dla aplikacji usługi Azure AD można wysłać ważne informacje o użytkowniku, aby było wstępnie wypełnić swojego konta formularza lub całkowicie wyeliminować.  Użytkownicy mogą rejestrować się w aplikacji przy użyciu konta usługi Azure AD za pomocą znanych zgody środowisko toothose podobne, znalezionych w mediów społecznościowych i aplikacji dla urządzeń przenośnych.  Każdy użytkownik może zarejestrować się i zaloguj tooan aplikacji, która jest zintegrowany z usługą Azure AD bez konieczności zaangażowania IT.  Dowiedz się więcej o [zarejestrowanie się aplikacji dla usługi Azure AD konto logowania](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Przeglądaj w poszukiwaniu użytkowników, zarządzanie Inicjowanie obsługi użytkowników i kontroli dostępu tooYour aplikacji
**Wyszukaj użytkowników w katalogu hello.**  Użyj hello interfejsu API programu Graph toohelp użytkowników wyszukiwania i przeglądania dla innych osób w organizacji, gdy zapraszanie innych osób lub udzielanie dostępu, zamiast je tootype adresów e-mail.  Użytkownicy mogą przeglądać przy użyciu interfejsu Styl książki znanych adresów, w tym wyświetlanie szczegółów hello hello hierarchii.  Dowiedz się więcej o hello [interfejsu API programu Graph](active-directory-graph-api.md).

**Ponowne wykorzystywanie grup usługi Active Directory i list dystrybucyjnych, który klienta jest już zarządzany.**  Usługi Azure AD zawiera grupy powitania klienta jest już przy użyciu dystrybucji poczty e-mail i zarządzanie dostępem.  Przy użyciu interfejsu API programu Graph hello, ponownego użycia tych grup, zwalniając użytkownika toocreate klienta i zarządzanie nimi osobne zestawy grup w aplikacji.  Informacje o grupie mogą być również wysyłane tooyour aplikacji w logowania tokenów.  Dowiedz się więcej o hello [interfejsu API programu Graph](active-directory-graph-api.md).

**Za pomocą usługi Azure AD toocontrol, kto ma dostęp do aplikacji tooyour.**  Administratorzy i właściciele aplikacji w usłudze Azure AD można przypisać dostępu tooapplications toospecific użytkowników i grup.  Przy użyciu interfejsu API programu Graph hello, można odczytać tej listy i użyciu toocontrol aprowizację i anulowanie obsługi zasobów, a dostęp w aplikacji.

**Kontrola dostępu oparta na użycie usługi Azure AD dla ról.**  Administratorzy i właściciele aplikacji można przypisać użytkowników i grup tooroles, który definiuje podczas rejestrowania aplikacji w usłudze Azure AD.  Informacje o rolach tooyour aplikacji do logowania tokenów, a także mogą być odczytywane przy użyciu hello interfejsu API programu Graph.  Dowiedz się więcej o [przy użyciu usługi Azure AD, do autoryzacji](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Pobierz profil tooUser dostępu, kalendarza, poczty E-mail, kontakty, plików i więcej
**Usługi Azure AD jest powitania serwera autoryzacji dla usługi Office 365 i innych usług biznesowych firmy Microsoft.**  Jeśli są używane usługi Azure AD podczas logowania w aplikacji tooyour lub łączenie bieżącego użytkownika konta tooAzure AD kont użytkowników przy użyciu protokołu OAuth 2.0 pomocy technicznej może wysłać żądanie odczytu i zapisu tooa użytkownika profilu, kalendarza, poczty e-mail, kontakty, plików i innych informacji.  Można bezproblemowo toouser zdarzenia kalendarza, zapisu i odczytu i zapisu tootheir plików usługi OneDrive.  Dowiedz się więcej o [podczas uzyskiwania dostępu do hello interfejsami API usługi Office 365](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Twoja aplikacja w hello Azure i Office 365 rynków
**Podwyższ poziom toohello miliony Twojej aplikacji organizacji, które już używają usługi Azure AD.**  Użytkownicy, którzy wyszukiwania i Przeglądaj tych rynków już jest używany jeden lub więcej usług w chmurze, dzięki czemu kwalifikowaną klienci usługi w chmurze.  Dowiedz się więcej o aplikacji w [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Przy rejestrowaniu użytkowników aplikacji pojawi się w ich panel dostępu usługi Azure AD i uruchamiania aplikacji usługi Office 365.**  Użytkownicy będą mogli tooquickly i łatwo zwracany tooyour aplikacji później, poprawy stopnia zaangażowania użytkowników.  Dowiedz się więcej o hello [panel dostępu usługi Azure AD](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Zabezpieczenia komunikacji usługi urządzeń i usług
**Używanie programu Azure AD do zarządzania tożsamościami, usług i urządzeń zmniejsza hello kod należy toowrite i umożliwia dostęp toomanage IT.**  Usługi i urządzenia można uzyskać tokenów z usługi Azure AD przy użyciu protokołu OAuth i użyć tych tokenów tooaccess interfejsów API sieci web.  Używanie programu Azure AD można uniknąć pisania kodu uwierzytelniania złożonego.  Ponieważ hello tożsamości, urządzeń i usług hello są przechowywane w usłudze Azure AD, IT mogą zarządzać kluczami i odwołania w jednym miejscu zamiast toodo to oddzielnie w aplikacji.

## <a name="benefits-of-integration"></a>Korzyści wynikające z integracji
Integracja z usługą Azure AD jest dostarczany z korzyści, które nie wymagają toowrite dodatkowy kod.

### <a name="integration-with-enterprise-identity-management"></a>Integracja z usługą zarządzania tożsamościami w przedsiębiorstwie
**Pomoc aplikacji są zgodne z zasadami IT.**  Organizacje zintegrować ich systemy zarządzania tożsamościami przedsiębiorstwa z usługą Azure AD, gdy osoba opuszcza organizację, automatycznie utracą dostęp do aplikacji tooyour bez tootake wymagających IT dodatkowych czynności.  IT można zarządzać, kto może uzyskać dostępu do aplikacji i określić, które zasady dostępu są wymagane — przykład uwierzytelnianie wieloskładnikowe - zmniejszenie Twoje potrzeby toowrite kodu toocomply z zasadami firmy złożonych.  Usługa Azure AD zapewnia administratorów z dziennika inspekcji szczegółowe kto zalogowany aplikacji tooyour tak IT mogą śledzić użycie.

**Usługi Azure AD rozszerza chmury toohello usługi Active Directory, aby aplikację można zintegrować z usługą Active Directory.**  W wielu organizacjach wokół Witaj świecie korzystania z usługi Active Directory jako ich główna logowania i system zarządzania tożsamościami i wymaga ich toowork aplikacji z usługą Active Directory.  Integracja z usługą Azure AD integruje się z usługą Active Directory aplikacji.

### <a name="advanced-security-features"></a>Funkcje zaawansowane zabezpieczenia
**Uwierzytelnianie wieloskładnikowe.**  Usługa Azure AD zapewnia natywnego uwierzytelnianie wieloskładnikowe.  Administratorzy IT mogą wymagać z usługi Multi-Factor authentication tooaccess aplikacji, dzięki czemu nie trzeba toocode ta obsługa samodzielnie.  Dowiedz się więcej o [uwierzytelnianie wieloskładnikowe](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Nietypowe logowania wykrywania.**  Usługi Azure AD przetwarza logowania ponad miliard dziennie, używając maszyny nauki algorytmów toodetect podejrzanych działań i powiadamiania administratorów IT o potencjalnych problemach.  Dzięki obsłudze logowania w usłudze Azure AD, aplikacja pobiera korzyści hello tej ochrony. Dowiedz się więcej o [wyświetlanie raportów dostępu do usługi Azure Active Directory](../active-directory-view-access-usage-reports.md).

**Dostęp warunkowy.**  Ponadto toomulti Multi-Factor authentication, Administratorzy mogą wymagać określonych warunków zostać spełnione, aby użytkownicy mogą logowania tooyour aplikacji.  Warunki, które można ustawić obejmują hello zakres adresów IP z urządzeń klienckich, członkostwo w określonych grup i stan hello hello urządzenia używane dla dostępu.  Dowiedz się więcej o [dostępu warunkowego w usłudze Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Łatwość programowania
**Standardowych protokołach branżowych.**  Firma Microsoft dokłada standardy branżowe toosupporting zatwierdzone.  Usługi Azure AD obsługuje protokoły uwierzytelniania hello SAML 2.0, OpenID Connect 1.0 OAuth 2.0 i WS-Federation 1.2.  Interfejs API programu Graph Hello jest OData 4.0 zgodne.  Jeśli aplikacja już obsługuje hello SAML 2.0 lub protokoły OpenID Connect 1.0 federacyjnym w celu logowania się, może być proste dodanie obsługi dla usługi Azure AD.  Dowiedz się więcej o [usługi Azure AD obsługiwane protokoły uwierzytelniania](active-directory-authentication-protocols.md).

**Biblioteki typu open source.**  Firma Microsoft udostępnia biblioteki w pełni obsługiwane typu open source dla rozwoju toospeed popularnych języków i platform.  Kod źródłowy Hello jest licencją Apache 2.0 i są toofork wolnego i współtworzenia wstecz toohello projektów.  Dowiedz się więcej o [biblioteki uwierzytelniania usługi Azure AD](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Obecność na całym świecie i wysokiej dostępności
**Usługi Azure AD jest wdrażana w centrach danych na całym świecie hello zarządzane i które są monitorowane wokół hello zegara.**  Usługi Azure AD to system zarządzania tożsamościami hello platformy Microsoft Azure i usługi Office 365 i jest wdrożona w 28 centrach danych wokół hello world.  Katalog danych jest gwarantowana toobe replikowane tooat co najmniej trzech w centrach danych.  Moduły równoważenia obciążenia globalnego upewnij się, użytkownicy uzyskują dostęp do hello najbliższego kopię usługi Azure AD zawierające dane, i automatycznie przekierowuje żądania tooother centrów danych, jeśli zostanie wykryty problem.

## <a name="next-steps"></a>Następne kroki
[Wprowadzenie do pisania kodu](active-directory-developers-guide.md#get-started).

[Loguj użytkowników przy użyciu usługi Azure AD](active-directory-authentication-scenarios.md)

