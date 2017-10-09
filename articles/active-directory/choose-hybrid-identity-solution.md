---
title: "aaaChoose rozwiązania z tożsamością hybrydową Azure | Dokumentacja firmy Microsoft"
description: "Uzyskaj podstawową wiedzę na temat rozwiązań tożsamości dostępne hybrydowego hello i zalecenia dotyczące możesz toomake hello najlepsze tożsamości ładu decyzja dla danej organizacji."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Microsoft hybrydowych rozwiązań tożsamości
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) hybrydowych rozwiązań tożsamości włączyć toosynchronize obiektów katalogu lokalnego z usługą Azure AD nadal użytkowników lokalnej i zarządzania nimi. Witaj pierwszy toomake decyzji podczas planowania toosynchronize Twojego lokalnymi Windows Server Active Directory z usługą Azure AD jest mają toouse synchronizacji tożsamości i tożsamości federacyjnych. Tożsamości synchronizowane i opcjonalnie skrótów haseł, użytkownicy toouse hello tego samego hasła tooaccess zarówno lokalnie, jak i oparte na chmurze zasobów organizacji. Bardziej zaawansowane wymagania scenariusz, na przykład-jednokrotnej (SSO) lub lokalnej usługi MFA należy toodeploy Active Directory Federation Services (AD FS) toofederate tożsamości. 

Dostępnych jest kilka opcji dostępne w celu konfigurowania tożsamości hybrydowej. Ten artykuł zawiera informacje o toohelp, wybrane hello najlepszy dla organizacji, łatwość wdrażania w oparciu i wymaga określonych zarządzania tożsamościami i dostępem. Podczas planowania model tożsamości, który najlepiej odpowiada potrzebom organizacji, należy również toothink o czasie, istniejącej infrastruktury, złożoność i kosztów. Czynniki te są różne dla każdej organizacji i może ulec zmianie. Jednak w przypadku zmiany wymagań, masz również hello elastyczność tooswitch tooa tożsamości innego modelu.

> [!TIP]
> Te rozwiązania są dostarczane przez [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Tożsamości synchronizowane 
Tożsamości synchronizowane jest hello najprostszy sposób toosynchronize lokalnych obiektów katalogu (użytkowników i grup) z usługą Azure AD. 

![Tożsamość hybrydowa zsynchronizowane](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Tożsamości synchronizowane jest metoda Najłatwiejszym i najszybszym hello, użytkownicy nadal muszą toomaintain oddzielnych haseł dla zasobów w chmurze. tooavoid, możesz również (opcjonalnie) [synchronizacji skrótów haseł użytkowników](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) katalogu tooyour usługi Azure AD. Synchronizowanie haseł skrótów umożliwia użytkownikom toolog w podstawie toocloud zasobów organizacji z hello tej samej nazwy użytkownika i hasła, że używają one lokalnymi. Azure AD Connect okresowo sprawdza zmiany i przechowuje zsynchronizowany katalog usługi Azure AD w katalogu lokalnym. Atrybut użytkownika lub hasło jest zmienione w lokalnej usłudze Active Directory, jest automatycznie aktualizowany w usłudze Azure AD. 

W przypadku większości organizacji, którzy potrzebują tylko tooenable ich toosign użytkowników w tooOffice 365 aplikacji SaaS i innych zasobów platformy Azure AD na podstawie opcji synchronizacji haseł domyślnej hello jest zalecane. Jeśli to nie pomoże Ci, konieczne będzie toodecide między uwierzytelniania przekazywanego i usług AD FS.

> [!TIP]
> Hasła użytkowników są przechowywane w lokalnych Windows Server Active Directory w formie hello wartość skrótu, która reprezentuje hello rzeczywistego hasła. Wartość skrótu jest wynikiem jednokierunkowej funkcji matematycznych (hello algorytmem wyznaczania wartości skrótu). Nie ma żadnych wyników hello toorevert metody w wersji jednokierunkowa funkcja toohello zwykłego tekstu hasła. Nie można użyć toosign skrótu hasła tooyour sieci lokalnej. Jeśli zrezygnujesz hasła toosynchronize skrótów haseł wyodrębnia Azure AD Connect z hello lokalnej usługi Active Directory i stosuje zabezpieczeń dodatkowego przetwarzania toohello skrót hasła, zanim zostanie zsynchronizowany tooAzure AD. Synchronizację haseł można również wraz z hasłem tooenable zapisu samodzielnego resetowania haseł w usłudze Azure AD. Ponadto umożliwia logowanie jednokrotne (SSO) dla użytkowników na komputerach przyłączonych do domeny, które są połączone toohello sieci firmowej. Z logowania jednokrotnego, włączone użytkownicy potrzebują tylko tooenter username toosecurely dostęp do zasobów chmury. 

## <a name="pass-through-authentication"></a>Przekazywanego uwierzytelniania
[Uwierzytelnianie usługi Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) zapewnia rozwiązanie weryfikacji proste hasło do usług platformy Azure na podstawie usługi AD przy użyciu lokalnej usługi Active Directory. Jeśli zasady zabezpieczeń i zgodności w firmie nie zezwalają na wysyłanie hasła użytkowników, nawet w formie skrótu i pulpitu toosupport SSO wystarczy tylko dla urządzeń przyłączonych do domeny, zaleca się przy użyciu uwierzytelniania przekazywanego oceny. Uwierzytelniania przekazywanego nie wymaga żadnych wdrożenia w hello DMZ, co upraszcza hello infrastruktura wdrażania w porównaniu z usługami AD FS. Podczas logowania przy użyciu usługi Azure AD, ta metoda uwierzytelniania sprawdza poprawność haseł użytkowników bezpośrednio z lokalnej usługi Active Directory.

![Przekazywanego uwierzytelniania](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Przy użyciu przekazywanego uwierzytelniania nie istnieje potrzeba złożoną siecią infrastruktury, a nie ma potrzeby toostore hasłami lokalnymi w chmurze hello. Połączone z logowania jednokrotnego, uwierzytelnianie przekazywane zapewnia obsługę naprawdę zintegrowanego przy logowaniu się w tooAzure AD lub innych usług w chmurze.

Przekazywanego uwierzytelniania jest skonfigurowane z programem Azure AD Connect, używający agenta proste lokalnymi, która nasłuchuje żądań sprawdzania poprawności hasła. Hello agenta można łatwo wdrożonej toomultiple maszyny tooprovide wysoką dostępność i równoważenie obciążenia. Ponieważ cała komunikacja jest tylko ruchu wychodzącego, nie jest wymagane dla toobe łącznika hello zainstalowany w strefie DMZ. wymagania dotyczące komputera serwera Hello łącznika hello są następujące:

- Windows Server 2012 R2 lub nowszy
- Dołączany do domeny w lesie hello za pomocą którego użytkownicy są weryfikowane tooa

> [!NOTE]
> Azure AD uwierzytelnianie przekazywane jest obecnie w wersji zapoznawczej i jest obsługiwana dla klientów przeglądarki sieci web i klientom pakietu Office, które obsługują nowoczesnego uwierzytelniania. Dla klientów, które nie są obsługiwane takie jak starszej wersji pakietu Office i programu Exchange ActiveSync (w tym klientów natywnych poczty e-mail na urządzeniach przenośnych), jest zalecane toouse hello nowoczesnego uwierzytelniania równoważne. Nowoczesnego uwierzytelniania nie umożliwia uwierzytelnianie przekazywane tylko umożliwia również zastosować, takich jak uwierzytelnianie wieloskładnikowe toobe zasady dostępu warunkowego. 

Przekazywanego uwierzytelniania nie jest obecnie obsługiwane, gdy przy użyciu urządzeń z systemem Windows 10 przyłączonych do tooAzure AD. Jednak synchronizacji skrótu hasła można użyć jako automatyczne toosupport rezerwowy systemu Windows 10 i wspomniano hello starszych klientów. Podczas podglądu hello synchronizacji skrótu hasła jest domyślnie włączona po wybraniu uwierzytelnianie przekazywane jako hello opcji logowania w programie Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Tożsamości federacyjnych (AD FS)
Aby uzyskać większą kontrolę nad dostęp użytkowników usługi Office 365 i innych usług w chmurze, można skonfigurować synchronizacji katalogów z logowaniem jednokrotnym (SSO) przy użyciu [Active Directory Federation Services (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Federowania logowania użytkownika z usług AD FS delegatów uwierzytelniania tooan lokalnego serwera, która weryfikuje poświadczenia użytkownika. W tym modelu lokalnej usługi Active Directory poświadczenia nigdy nie są przekazywane tooAzure AD.

![Tożsamości federacyjnych](./media/choose-hybrid-identity-solution/federated-identity.png)

Zwanej również Federacją tożsamości, ta metoda logowania zapewnia, że wszystkie uwierzytelnianie użytkownika jest kontrolowany lokalnymi i pozwala administratorom tooimplement bardziej rygorystyczne poziomy kontroli dostępu. Federacji tożsamości z usługami AD FS jest opcja hello najbardziej skomplikowane i wymaga wdrażania dodatkowych serwerów w środowisku lokalnym. Federacji tożsamości zatwierdza również tooproviding 24 x 7 obsługę infrastruktury usługi Active Directory i usług AD FS. Tak wysokiego poziomu obsługi jest konieczne, ponieważ jeśli internetowy lokalnymi, kontroler domeny lub serwery usług AD FS są niedostępne, użytkownicy nie mogą się zalogować w toocloud usług.

> [!TIP]
> Jeśli zdecydujesz się toouse federacji z usługi Active Directory Federation Services (AD FS), można opcjonalnie skonfigurować synchronizacji haseł jako zapasowy na wypadek awarii infrastruktury usług AD FS.


## <a name="common-scenarios-and-recommendations"></a>Typowe scenariusze i zalecenia
Poniżej przedstawiono niektóre typowe tożsamość hybrydowa i scenariuszy zarządzania dostępu na podstawie zaleceń jako opcja tożsamość hybrydowa toowhich (lub opcji) może być odpowiednie dla każdego.

|Należy:|PWS i logowania jednokrotnego<sup>1</sup>| PTA i logowania jednokrotnego<sup>2</sup> | USŁUGI AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Synchronizacja nowych, skontaktuj się z pomocą, konta użytkowników i grup tworzone automatycznie w mojej lokalnej usługi Active Directory toohello chmury.|![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)| ![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png) |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Skonfiguruj moje dzierżawy w scenariuszach hybrydowych usługi Office 365|![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)| ![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png) |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Włącz toosign Moje użytkowników w i dostęp do usługi w chmurze przy użyciu swoich haseł lokalnych|![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)| ![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png) |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Implementowanie logowania jednokrotnego przy użyciu poświadczeń firmowych|![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)| ![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png) |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Upewnij się, że hasła nie są przechowywane w chmurze hello| |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Włącz uwierzytelnianie wieloskładnikowe rozwiązań lokalnymi| | |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|Obsługa uwierzytelniania za pomocą kart inteligentnych dla moich użytkowników<sup>4</sup>| | |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|
|W portalu usługi Office hello i na pulpicie systemu Windows 10 hello na wyświetlanie powiadomień wygaśnięcia hasła| | |![Zalecane](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> synchronizacji haseł z logowania jednokrotnego. 

> <sup>2</sup> przekazywanego uwierzytelniania i logowania jednokrotnego. 

> <sup>3</sup> federacyjne logowanie jednokrotne z usługami AD FS.

> <sup>4</sup> usług AD FS można zintegrować z Twojej tooallow infrastruktura PKI przedsiębiorstwa Zaloguj się przy użyciu certyfikatów. Te certyfikaty mogą być elastyczne certyfikatów wdrożonych za pośrednictwem zaufanego inicjowania obsługi administracyjnej kanałów, takich jak certyfikaty zarządzania urządzeniami Przenośnymi lub zasad grupy lub za pomocą kart inteligentnych (w tym karty PIV/CAC) lub Hello dla firm (relacji zaufania certyfikatów). Aby uzyskać więcej informacji na temat obsługi uwierzytelniania za pomocą kart inteligentnych, zobacz [ten blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej w środowisku Azure koncepcji](https://aka.ms/aad-poc)

[Instalowanie programu Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[Monitor synchronizacji tożsamości hybrydowej](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

