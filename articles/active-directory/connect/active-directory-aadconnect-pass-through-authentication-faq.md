---
title: "Azure AD Connect: Przekazywanego uwierzytelniania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Toofrequently odpowiedzi zadawane pytania dotyczące uwierzytelniania przekazywanego Azure Active Directory."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Azure Active Directory przekazywanego uwierzytelniania: Często zadawane pytania

W tym artykule można rozwiązać często zadawane pytania dotyczące usługi Azure Active Directory (Azure AD) przekazywanego uwierzytelniania. Sprawdzanie wstecz dla nowej zawartości.

>[!IMPORTANT]
>funkcja uwierzytelniania przekazywanego Hello jest obecnie w przeglądzie.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Które hello Azure AD metody logowania - przekazywanego uwierzytelniania, synchronizacji skrótów haseł i Active Directory Federation Services (AD FS) — należy wybrać?

Go zależy od lokalnego środowiska i wymagań organizacyjnych. Ten artykuł, aby przejrzeć [porównanie hello różne metody logowania usługi Azure AD](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>Jest bezpłatne funkcji uwierzytelniania przekazywanego?

Przekazywanego uwierzytelniania jest funkcją wolnego i nie wymagają żadnych płatnej wersji usługi Azure AD toouse go. Nadal pozostaje wolny, gdy funkcja hello osiągnie ogólnej dostępności.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>Jest dostępna w uwierzytelniania przekazywanego [Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) i [Microsoft Azure dla instytucji rządowych Cloud](https://azure.microsoft.com/features/gov/)?

Nie, przekazywanego uwierzytelniania jest dostępna tylko w Witaj świecie wystąpienia usługi Azure AD.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>Jest [dostępu warunkowego](../active-directory-conditional-access.md) pracy przy użyciu uwierzytelniania przekazywanego?

Tak, wszystkie możliwości dostępu warunkowego, w tym Azure Multi-Factor Authentication działa przy użyciu uwierzytelniania przekazywanego.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Uwierzytelniania przekazywanego obsługuje "Alternatywnego Identyfikatora" jako nazwy użytkownika hello, zamiast "userPrincipalName"?

Tak. Obsługuje uwierzytelniania przekazywanego `Alternate ID` jako hello nazwy użytkownika, gdy skonfigurowane w programie Azure AD Connect, jak pokazano [tutaj](active-directory-aadconnect-get-started-custom.md). Nie wszystkie aplikacje usługi Office 365 obsługują `Alternate ID`. Zapoznaj się z dokumentacją toohello określonej aplikacji hello obsługi instrukcji.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Synchronizacja skrótów haseł działać jako uwierzytelniania rezerwowego tooPass przez?

Nie, synchronizacji skrótu hasła nie jest ogólny tooPass do uwierzytelniania rezerwowego. Działa tylko jako rezerwowe dla [scenariusze uwierzytelniania przekazywanego nie obsługuje obecnie](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid użytkownika błędów logowania, należy skonfigurować uwierzytelniania przekazywanego [wysokiej dostępności](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>Można zainstalować [serwera Proxy aplikacji usługi Azure AD](../active-directory-application-proxy-get-started.md) łącznika na powitania tym samym serwerze co Agent uwierzytelniania przekazywanego?

Tak, ta konfiguracja jest obsługiwana z hello rebranded wersji hello Agent uwierzytelniania przekazywanego (wersje 1.5.193.0 lub nowszej).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>Które wersje programu Azure AD Connect i Agent uwierzytelniania przekazywanego potrzebujesz?

Wymagana wersja 1.1.486.0 później w celu Azure AD Connect i 1.5.58.0 lub nowszym w przypadku hello Agent uwierzytelniania przekazywanego do toowork tej funkcji. Całe oprogramowanie należy zainstalować na serwerach z systemem Windows Server 2012 R2 lub nowszym.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>Co się stanie, jeśli upłynął hasło tego użytkownika i spróbuj toosign przy użyciu uwierzytelniania przekazywanego?

Jeśli skonfigurowano [funkcji zapisywania zwrotnego haseł](../active-directory-passwords-update-your-own-password.md) dla określonego użytkownika, a jeśli hello użytkownik loguje się przy użyciu przekazywanego uwierzytelniania, można zmienić lub resetowanie haseł. Witaj hasła są zapisywane tooon lokalnej usłudze Active Directory zgodnie z oczekiwaniami.

Jednak jeśli nie skonfigurowano funkcję zapisywania zwrotnego haseł dla określonego użytkownika lub hello użytkownik nie ma prawidłową usługi Azure AD licencją, hello użytkownika nie może zaktualizować swoje hasło w chmurze hello. Nie można ich zaktualizowania hasła, nawet jeśli ich hasło wygasło. Witaj użytkownik widzi zamiast tego komunikatu: "Twoja organizacja nie zezwala tooupdate hasło w tej witrynie. Zaktualizuj go zgodnie z metodą toohello zalecaną przez organizację lub poproś administratora w celu uzyskania pomocy." Witaj, użytkownik lub hello administrator ma tooreset swoje hasło w lokalnej usługi Active Directory.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>Sposób uwierzytelniania przekazywanego chroni jednak przed atakami siłowymi hasło?

Odczyt [w tym artykule](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) Aby uzyskać więcej informacji.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>Co agentów uwierzytelniania przekazywanego komunikacji za pośrednictwem portów 80 i 443?

- Agentów uwierzytelniania Hello tworzą żądania HTTPS przez port 443 dla wszystkich operacji funkcji.
- Agenci uwierzytelniania Hello należy żądań HTTP za pośrednictwem portu 80 toodownload SSL list odwołania certyfikatów.

     >[!NOTE]
     >Firma Microsoft zmniejszeniu hello liczby portów wymaganych przez funkcję hello najnowsze aktualizacje. Jeśli masz starsze wersje usługi Azure AD Connect lub hello Agent uwierzytelniania, nie zamykaj tych portów również: 5671, 8080, 9090, 9091, 9350, 9352 i 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Można agentów uwierzytelniania przekazywanego hello komunikują się za pośrednictwem serwera proxy ruchu wychodzącego sieci web?

Tak. WPAD (Web autowykrywania serwera Proxy) jest włączona w środowisku lokalnym, agenci uwierzytelniania automatycznie podejmować toolocate i używać serwera proxy sieci web w sieci hello.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>Można zainstalować dwóch lub więcej agentów uwierzytelniania przekazywanego na hello tego samego serwera?

Nie, tylko można zainstalować jeden Agent uwierzytelniania przekazywanego na jednym serwerze. Tooconfigure uwierzytelniania przekazywanego wysoką dostępność, należy wykonać instrukcje hello na tym [artykułu](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) zamiast tego.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Już używać usług federacyjnych Active Directory (AD FS) do logowania w usłudze Azure AD. Jak przełączać jej tooPass przez uwierzytelniania?

Jeśli usługi AD FS zostały skonfigurowane jako metodę logowania za pomocą kreatora Połącz hello Azure AD, zmiana metody logowania użytkownika hello tooPass do uwierzytelniania. Ta zmiana umożliwia użycie uwierzytelniania przekazywanego hello dzierżawcy i konwertuje _wszystkie_ Sfederowanych domen w domenach zarządzanych. Wszystkie kolejne żądania rejestracji w dzierżawie są obsługiwane przez uwierzytelniania przekazywanego. Obecnie nie jest żadnym obsługiwanych w ciągu toouse Azure AD Connect kombinacji uwierzytelniania przekazywanego i usług AD FS w różnych domenach.

Jeśli usługi AD FS został skonfigurowany jako metoda logowania hello _poza_ hello Azure AD Connect kreatora, należy zmienić metody logowania użytkownika hello tooPass do uwierzytelniania (w tym opcję "Nie należy konfigurować" hello). Ta zmiana umożliwia użycie uwierzytelniania przekazywanego hello dzierżawcy. Jednak wszystkie domeny federacyjne nadal toouse usług AD FS dla logowania. Użyj programu PowerShell toomanually przekonwertować niektórych lub wszystkich tych Sfederowanych domen tooManaged domen. Po utworzeniu tego żądania wszystkich logowanie w domenach zarządzanych (_tylko_) są obsługiwane przez funkcję uwierzytelniania przekazywanego.

>[!IMPORTANT]
>Uwierzytelniania przekazywanego nie obsługuje logowania tylko w chmurze Azure AD users.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>W środowisku wielu lasów usługi AD można używać uwierzytelniania przekazywanego?

Tak. Środowiska z wieloma lasami są obsługiwane, jeśli istnieją relacje zaufania lasu między z lasów usługi AD i Jeśli routing sufiksów nazw jest poprawnie skonfigurowany.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Czy agenci uwierzytelniania przekazywanego mają możliwość równoważenia obciążenia?

Nie, instalowanie wielu agentów uwierzytelniania przekazywanego zapewnia [wysokiej dostępności](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), ale nie Równoważenie obciążenia. Jedno lub dwa hello uwierzytelniania agentów może się okazać zbiorczego hello hello logowania żądań obsługi.

Żądania weryfikacji haseł, które hello toohandle konieczność czynników uwierzytelniania są lightweight. W związku z tym maksymalne i średnie obciążenie dla większości klientów łatwo jest obsługiwany przez dwóch lub trzech agentów uwierzytelniania w sumie.

Zaleca się zainstalowanie agentów uwierzytelniania Zamknij tooyour kontrolerów domeny tooimprove logowania opóźnienia.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Można zainstalować hello pierwszego przekazywanego uwierzytelniania agenta na serwerze innym niż hello, który uruchamia Azure AD Connect?

Nie, ten scenariusz jest _nie_ obsługiwane.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Ile agentów uwierzytelniania przekazywanego należy zainstalować?

Zalecamy, aby:

- Całkowita liczba należy zainstalować dwóch lub trzech agentów uwierzytelniania. Ta konfiguracja jest odpowiednia dla większości klientów.
- Należy zainstalować agentów uwierzytelniania na kontrolerach domeny (lub jako Zamknij toothem, jak to możliwe) tooimprove logowania opóźnienia.
- Upewnij się, że serwery (w których zostali zainstalowani agenci uwierzytelniania) są dodane toohello AD tego samego lasu jako hello użytkowników, których hasła muszą toobe zweryfikowany.

>[!NOTE]
>Brak limitu systemowego 12 agentów uwierzytelniania dla każdego dzierżawcy.

## <a name="how-can-i-disable-pass-through-authentication"></a>Jak wyłączyć uwierzytelniania przekazywanego?

Ponownie uruchom Kreator Azure AD Connect hello i zmień metody logowania użytkownika hello z metody tooanother uwierzytelniania przekazywanego. Ta zmiana powoduje wyłączenie uwierzytelniania przekazywanego hello dzierżawcy i odinstalowuje hello Agent uwierzytelniania z powitania serwera. Masz toomanually hello Odinstaluj agentów uwierzytelniania z innych serwerów.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>Co się stanie, gdy odinstalować agenta uwierzytelniania przekazywanego?

Dezinstalacja agenta uwierzytelniania przekazywanego z serwerem powoduje, że go toostop akceptować żądania logowania. Upewnij się, że masz innego agenta uwierzytelniania uruchomionego przed wykonaniem tej operacji, tooavoid fundamentalne użytkownika logowania w dzierżawie.

## <a name="next-steps"></a>Następne kroki
- [**Bieżące ograniczenia** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — ta funkcja jest obecnie w przeglądzie. Dowiedz się, jakie scenariusze są obsługiwane i zostały.
- [**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.
- [**Nowości techniczne** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
