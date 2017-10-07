---
title: "aaaAzure Active Directory fazy weryfikacji koncepcji podręcznika dotyczącego implementacji | Dokumentacja firmy Microsoft"
description: "Eksploruj i szybkie rozpoczęcie scenariusze Zarządzanie tożsamościami i dostępem"
services: active-directory
keywords: "Usługa Azure active directory, podręcznika dotyczącego koncepcji, aby zapewnić"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Dowód koncepcji podręcznika dotyczącego usługi Azure Active Directory: implementacja

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation — synchronizowanie AD tooAzure AD 

Tożsamość hybrydowa jest hello foundation dla większości hello enterprise klientów, którzy mają już katalog lokalny. Witaj celem jest toointentionally poświęcają jako mniej czasu, w tym miejscu jako wartość hello możliwe tooshow hello rzeczywistych scenariuszy tożsamościami i dostępem. 

| Scenariusz | Bloki konstrukcyjne| 
| --- | --- |  
| [Rozszerzanie lokalnej tożsamości toohello chmury](#extending-your-on-premises-identity-to-the-cloud) | [Synchronizacja katalogów — synchronizacja skrótów haseł](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Uwaga**: Jeśli masz już DirSync/ADSync i jego wcześniejsze wersje programu Azure AD Connect, ten krok jest opcjonalny. Sytuacje, w tym przewodniku może wymagać nowszej wersji programu Azure AD Connect.  <br/>[Znakowania.](active-directory-playbook-building-blocks.md#branding) | 
| [Przypisywanie licencji usługi Azure AD przy użyciu grup](#assigning-azure-ad-licenses-using-groups) | [Oparta na grupy licencji](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Rozszerzanie lokalnej tożsamości toohello chmury 

1. Robert jest hello administratora usługi Active Directory w firmie Contoso. Pobiera on hello wymaganie tooenable tożsamości, jako usługa dla zestawu użytkowników. Po wykonaniu Kreator Azure AD Connect, tożsamość hello hello użytkowników docelowych dostępna w chmurze hello. 
2. Robert zapyta Susie, jeden z użytkowników docelowych hello, tooaccess hello panel dostępu usługi Azure Active Directory i upewnij się, że użytkownik może uwierzytelnić. Susie widzi strony marką logowania i panelu dostępu puste, który jest gotowy do włączania dostępu do aplikacji w przyszłości.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Przypisywanie licencji usługi Azure AD przy użyciu grup 

1. Robert jest hello Azure AD administratora globalnego i chce tooallocate usługi Azure AD licencji tooa określonych użytkowników w ramach hello początkowe wdrożenie usługi Azure AD.
2. Robert tworzy grupę na powitania użytkowników pilotażowych. 
3. Robert przypisuje hello licencji toohello grupy
4. Susie, jeden hello pracowników przetwarzających informacje, jest dodana grupa zabezpieczeń toohello jako część jej zadania
5. Po pewnym czasie Susie ma dostęp toohello usługi Azure AD premium licencji. Spowoduje to włączenie więcej scenariusze weryfikacji Koncepcji hello później.

## <a name="theme---lots-of-apps-one-identity"></a>Motyw — części aplikacji, co tożsamości

| Scenariusz | Bloki konstrukcyjne| 
| --- | --- |  
| [Integracja aplikacji SaaS - federacyjną rejestracją Jednokrotną](#integrate-saas-applications---federated-sso) | [Konfiguracja federacyjną rejestracją Jednokrotną w modelu SaaS](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Grupy - delegować prawa własności](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Integracja aplikacji SaaS — hasło logowania jednokrotnego](#integrate-saas-applications---password-sso) | [Konfiguracja rejestracji Jednokrotnej SaaS hasła](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [Usługa rejestracji Jednokrotnej i zdarzenia cyklu życia tożsamości](#sso-and-identity-lifecycle-events) | [SaaS i cyklem życia tożsamości](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Zabezpieczanie dostępu do kont tooShared](#secure-access-to-shared-accounts) | [SaaS kont konfiguracji udostępnionej](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Bezpieczne aplikacje lokalne tooOn dostępu zdalnego](#secure-remote-access-to-on-premises-applications) | [Konfiguracja serwera Proxy aplikacji](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [Synchronizuj LDAP tooAzure tożsamości usługi AD](#synchronize-ldap-identities-to-azure-ad) |  [Ogólny łącznik LDAP konfiguracji](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Integracja aplikacji SaaS - federacyjną rejestracją Jednokrotną 

1. Robert jest hello administratora globalnego usługi Azure AD i otrzymuje żądanie z hello Marketing działu tooenable dostępu tootheir wystąpienia usługi ServiceNow. Robert znajduje hello samouczek krok po kroku w dokumentacji usługi Azure AD i następuje i delegatów hello przypisania tooKevin aplikacji toohello użytkowników, head hello zespołu marketingu. 
2. Jan zaloguje się jako właściciel hello uprawnień usługi ServiceNow i przypisuje Susie toohello aplikacji. Jan powiadomienia, że jego Susie profil został utworzony w usługi ServiceNow automatycznie
3. Susie jest Pracownik przetwarzający informacje w dziale marketingu hello. Użytkownik zaloguje się tooazure AD i wyszukuje wszystkie aplikacje SaaS użytkownik jest przypisany tooin myapps portalu. Z tego miejsca klika bezproblemowo pobiera tooServiceNow dostępu.
4. Witaj działu marketingu chce tooaudit, który uzyskał dostęp do usługi ServiceNow. Robert pobiera raport aktywności i udostępnia ją Kevina za pośrednictwem poczty e-mail.  

### <a name="sso-and-identity-lifecycle-events"></a>Usługa rejestracji Jednokrotnej i zdarzenia cyklu życia tożsamości

1. Susie przyjmuje urlop i przez zasady firmowe hello lokalne konto usługi AD jest wyłączona tymczasowego. Susie nie może zalogować się tooAzure AD i dlatego nie można uzyskać dostępu do usługi ServiceNow. 
2. Susie sprawia, że penetracji przenoszenia obrotu tooSales. Jan usuwa jej dostępu usługi ServiceNow. Susie zaloguje hello myapps usługi azure ad, a nie widzi hello Kafelek usługi ServiceNow. Po 10 minutach Kevina potwierdza, że konto Susie zostało wyłączone z konsoli zarządzania usługi ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Integracja aplikacji SaaS — hasło logowania jednokrotnego

1. Robert konfiguruje tooAtlassian dostępu HipChat. HipChat ma hasło logowania jednokrotnego integracji i przyznać dostęp tooSusie
2. Susie dzienniki w portalu myapps toohello i widzi hello toodownload łącze rozszerzenia przeglądarki IE usługi Azure AD, która pobiera ona
3. Po kliknięciu, klika pobiera monitowani o podanie poświadczeń jej HipChat nazwy użytkownika i hasła. Jest to jednorazowa operacja i po jej zakończeniu ma tooHipChat dostępu
4. Później za kilka dni Susie otwiera myapps portalu i klika HipChat ponownie. Go pobiera ona bezproblemowy dostęp
5. Jan, właściciel aplikacji hello HipChat chce tooaudit, który uzyskał dostęp do aplikacji hello. Robert pobiera raport dotyczący inspekcji i udostępnia ją Kevina za pośrednictwem poczty e-mail. 

### <a name="secure-access-tooshared-accounts"></a>Zabezpieczanie dostępu do kont tooShared 

1. Robert jest zlecił toosecure hello udostępnionych Twitter obsługę członkowie zespołu sprzedaży hello. On dodaje Twitter jako aplikację rejestracji Jednokrotnej i przypisuje go grupy zabezpieczeń toohello hello zespół ds. sprzedaży. Został on podany hello poświadczenia toohello udostępnionego konta i on dostarcza hello systemu. 
2. Udostępnianie Twitter poświadczeń nie jest już zaufany powodu osób toomultiple wiedzy użytkownika. Robert umożliwia automatyczne Przerzucanie hello Twitter hasła.
3. Susie, członek zespołu sprzedaży hello, rejestruje w portalu myapps toohello i widzi hello toodownload łącze rozszerzenia przeglądarki IE usługi Azure AD. Użytkownik instaluje go.
4. Po kliknięciu ona get bezpośredni dostęp tooTwitter. Użytkownik nie zna hasło hello.
5. Arnold jest również częścią hello zespołu ds. Ma on hello same występują jako Susie w krokach 3 — 4
6. Pracownicy działu sprzedaży Hello chce tooaudit, który uzyskał dostęp do usługi Twitter. Robert pobiera raport aktywności i udostępnia ją Kevina za pośrednictwem poczty e-mail. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Bezpieczne aplikacje lokalne tooOn dostępu zdalnego

1. Bob hello Azure AD administratora globalnego, uzyskał wiele żądań tooenable pracowników tooaccess kilka przydatne lokalnych zasobów, takich jak hello kosztów aplikacji, podczas pracy zdalnej. Wykonuje hello [dokumentacji serwera Proxy aplikacji](active-directory-application-proxy-enable.md) tooinstall łącznika i opublikować kosztów jako aplikację serwera Proxy aplikacji. 
2. Robert udostępniać hello zewnętrzny URL aplikacji kosztów Susie, jeden hello pracowników, którzy wymaga dostępu zdalnego. Klika hello link uzyskuje dostęp do, a po uwierzytelniany w usłudze AAD, użytkownik jest tooaccess stanie hello kosztów aplikacji i kontynuować toobe produktywności podczas pracy zdalnej. 
3. Roberta, który następnie jest kontynuowana, że hello toopublish dodatkowych lokalnych aplikacji przy użyciu tego samego procesu i podając toousers dostępu, zgodnie z potrzebami. Dodaje dostępu warunkowego i uwierzytelniania wieloskładnikowego na powitania bardziej poufnego aplikacje, które on publikuje, tooensure dodatkowe zabezpieczenia.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>Synchronizuj LDAP tooAzure tożsamości usługi AD

1. Roberta firma ma infrastrukturę złożone tożsamości. Większość użytkowników hello są obsługiwane wewnątrz systemu Windows Server Active Directory domeny usługi (DODAJE). Niektóre z nich, są zarządzane przez system HR wewnątrz Active Directory Lightweight Directory Services (ADLDS).
2. Robert jest zlecił mu włączania dostępu tooSaaS aplikacji dla wszystkich użytkowników (także tych nie występują w DODAJE).
3. Robert konfiguruje danych toopull ogólny łącznik LDAP z ADLDS w programie Azure AD Connect.
4. Robert tworzy reguły synchronizacji, a więc LDAP użytkowników są umieszczane w Metaverse i tooAzure AD
5. Tożsamości synchronizowane Susie, która LDAP użytkownik uzyskuje dostęp do jej SaaS aplikacji w usłudze



> [!IMPORTANT] 
> Jest to Konfiguracja zaawansowana wymagające masz pewną znajomość programu FIM/MIM. Jeśli używane w środowisku produkcyjnym, zaleca się pytania dotyczące tej konfiguracji przejść przez [pomocy technicznej Premium](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Motyw — zwiększenie bezpieczeństwa 

| Scenariusz | Bloki konstrukcyjne| 
| --- | --- |  
| [Administrator bezpiecznego dostępu do konta](#secure-administrator-account-access) | [Usługa Azure MFA z połączeń telefonicznych](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Bezpieczny dostęp do aplikacji](#secure-access-to-applications) | [Dostęp warunkowy dla aplikacji SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Włącz tylko w czasie administracji](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Ochrona tożsamości oparte na ryzyko](#protect-identities-based-on-risk) | [Wykrywanie zdarzenia ryzyka](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Wdrażanie zasad logowania ryzyka](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Uwierzytelnianie bez hasła przy użyciu uwierzytelniania opartego na certyfikatach](#authenticate-without-passwords-using-certificate-based-authentication) | [Konfigurowanie uwierzytelniania opartego na certyfikatach](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Administrator bezpiecznego dostępu do konta

1. Robert jest hello Administrator globalny usługi Azure AD. Zidentyfikował on Stuart jako współadministrator hello usługi. 
2. Robert konfiguruje konto w Stuart tooalways wymagają usługi MFA tooimprove hello strukturę
3. Stuart loguje toohello portalu Azure i powiadomienia, że musi tooregister logowania hello toocontinue numer swojego telefonu
4. Kolejnych logowań z Stuart są teraz chronione przy użyciu uwierzytelniania wieloskładnikowego i on teraz pobiera tooverify rozmowy telefonicznej jego tożsamość.

### <a name="secure-access-tooapplications"></a>Bezpieczny dostęp tooapplications

1. Tomasz jest właścicielem firm hello usługi ServiceNow. Firma Hello teraz chce toologin tych użytkowników za pomocą usługi MFA, podczas uzyskiwania dostępu do sieci firmowej hello zewnętrznej.
2. Dostęp warunkowy zasad toohello usługi ServiceNow aplikacji tooenable uwierzytelnianie wieloskładnikowe dla dostępu poza dodaje Bob naszych administratora globalnego usługi Azure AD
3. Susie, naszych Pracownik przetwarzający informacje logowania w portalu Moje aplikacje i klika hello usługi ServiceNow kafelka. Teraz jest ona wezwał za pomocą usługi MFA.

### <a name="enable-just-in-time-jit-administration"></a>Włącz tylko w witrynie Administracja time (JIT)

1. Robert i Stuart są Administratorzy globalni usługi Azure AD. Tooenable JIT dostępu toohello zarządzania rolami i i również tookeep rekordów na użycie hello hello uprzywilejowany ról.
2. Robert włącza usługi PIM w dzierżawie usługi Azure AD hello i staje się administratorem zabezpieczeń hello. On zmienia się i członkostwo w roli administratora globalnego firmy Stuart tooeligible trwałych.
3. Robert i Stuart teraz wymagają aktywacji ich roli za pomocą hello portalu Azure, przed wykonaniem zmienia tooAzure AD konfiguracji. 

### <a name="protect-identities-based-on-risk"></a>Ochrona tożsamości oparte na ryzyko 

1. Susie, Pracownik przetwarzający informacje próbuje zalogować się przy użyciu przeglądarki tor. 
2. Robert sprawdza hello usługi Azure AD identity protection w pulpicie nawigacyjnym i widzi na Susie logowania z anonimowych adresów IP. Witaj zabezpieczeń zespół chce się, że toochallenge takie uzyskuje dostęp do użytkowników za pomocą usługi MFA
3. Robert umożliwia toochallenge usługi Azure AD Identity Protection zasad MFA dla zdarzeń o podwyższonym ryzyku średnia lub nowszej
4. Czas przechodzi i Susie dzienniki w przeglądarce Tor ponownie. Tym razem, użytkownik zostanie wyświetlony hello żądanie uwierzytelniania MFA

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Uwierzytelnianie bez hasła przy użyciu uwierzytelniania opartego na certyfikatach

1. Tomasz jest administratorem globalnym dla instytucji finansowej, który zabrania używania haseł jako składnik uwierzytelniania dla aplikacji.
2. Robert umożliwia i wymusza certyfikatów uwierzytelniania w usługach AD FS a usługą Azure AD
3. Susie podczas uzyskiwania dostępu do aplikacji zostanie wyświetlony monit tooauthenticate przy użyciu certyfikatu

## <a name="theme---scale-with-self-service"></a>Motyw — skali z samoobsługi

| Scenariusz | Bloki konstrukcyjne| 
| --- | --- |  
| [Samodzielne resetowanie haseł](#self-service-password-reset) | [Samodzielne resetowanie haseł](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [Samodzielnie tooApplications dostępu do usługi](#self-service-access-to-applications) | [Samodzielnie tooApplications dostępu do usługi](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Samodzielne resetowanie haseł 

1. Robert jest hello Azure AD globalnego administratora, jak i umożliwia zarządzanie hasłami usługi samoobsługowego tooa podzbiór użytkowników, w tym Susie. 
2. Susie dzienniki w portalu toomyapps i zobacz tooregister komunikat jej informacje o zabezpieczeniach dla resetowania hasła przyszłych zdarzeń.
3. Szybko przewiń do przodu za kilka dni Susie zapomni swoje hasło, a ponadto resetuje go za pomocą portalu usługi Azure AD

### <a name="self-service-access-tooapplications"></a>Samodzielnie tooApplications dostępu do usługi 

1. Tomasz jest właścicielem firm hello usługi ServiceNow. Maciej chce zbyt "tworzyć konta użytkowników" ją na żądanie, zamiast dodawania ich jednocześnie
2. Bob naszej usługi Azure AD administratora globalnego modyfikuje tooenable aplikacji usługi ServiceNow hello żądań samoobsługi
3. Susie, naszych Pracownik przetwarzający informacje rejestruje się w portalu Moje aplikacje i kliknięcia przycisku "Dodaj więcej aplikacji" hello i zobacz usługi ServiceNow wśród zalecane aplikacji hello. Następnie użytkownik nawiguje wstecz toomy aplikacji portalu i zobacz hello usługi ServiceNow aplikacji.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]