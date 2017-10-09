---
title: "Azure AD przekazywanego uwierzytelniania — Szybki Start | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób uruchamiania tooget przy użyciu uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)."
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Usługi Azure Active Directory przekazywanego uwierzytelniania: Szybki start

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Jak toodeploy Azure AD przekazywanego uwierzytelniania

Azure Active Directory (Azure AD) przekazywanego uwierzytelniania umożliwia toosign Twojego użytkowników w tooboth lokalnych i aplikacji opartych na chmurze za pomocą hello takich samych haseł. Go loguje się użytkowników weryfikując haseł bezpośrednio z lokalnej usługi Active Directory.

>[!IMPORTANT]
>Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie. Jeśli z tej funkcji za pomocą podglądu, należy upewnić się, uaktualnienie wersji zapoznawczych hello uwierzytelniania agentów przy użyciu instrukcji hello [tutaj](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

Należy toofollow toodeploy te instrukcje przekazywanego uwierzytelniania:

## <a name="step-1-check-prerequisites"></a>Krok 1: Sprawdź wymagania wstępne

Upewnij się, że hello następujące wymagania wstępne zostały spełnione:

### <a name="on-hello-azure-active-directory-admin-center"></a>W Centrum administracyjnym usługi Active Directory Azure hello

1. Utwórz konto administratora globalnego tylko w chmurze w dzierżawie usługi Azure AD. W ten sposób można zarządzać hello konfigurację dzierżawy powinna zakończyć się niepowodzeniem z lokalnymi usługami lub staną się niedostępne. Dowiedz się więcej o [dodanie konta administratora globalnego tylko w chmurze](../active-directory-users-create-azure-portal.md). Wykonanie tego kroku jest tooensure krytyczne, nie uzyskać blokady dzierżawy.
2. Dodaj jeden lub kilka [nazwy domeny niestandardowej](../active-directory-add-domain.md) dzierżawy tooyour usługi Azure AD. Użytkownicy logują się przy użyciu jednej z tych domen.

### <a name="in-your-on-premises-environment"></a>W środowisku lokalnym

1. Zidentyfikuj serwer z systemem Windows Server 2012 R2 lub nowszym na które toorun Azure AD Connect. Dodaj powitania serwera toohello AD tego samego lasu jako hello użytkowników, których hasła muszą toobe zweryfikowany.
2. Zainstaluj hello [najnowszą wersję programu Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) na powitania serwera określoną w poprzednim kroku. Jeśli masz już uruchomiona usługa Azure AD Connect, upewnij się, czy wersji hello jest 1.1.557.0 lub nowszym.
3. Zidentyfikuj dodatkowy serwer z systemem Windows Server 2012 R2 lub później na które toorun a autonomiczny Agent uwierzytelniania. Wersja agenta uwierzytelniania Hello musi toobe 1.5.193.0 lub nowszym. Ten serwer jest wymagane tooensure wysoką dostępność żądań logowania. Dodaj powitania serwera toohello AD tego samego lasu jako hello użytkowników, których hasła muszą toobe zweryfikowany.
4. W przypadku zapory między serwerami a usługą Azure AD, należy hello tooconfigure następujące elementy:
   - Upewnij się, czy agenci uwierzytelniania można wprowadzać **wychodzących** żądania tooAzure AD hello następujące porty:
   
   | Numer portu | Jak jest używany |
   | --- | --- |
   | **80** | Pobieranie odwołania certyfikatu list podczas sprawdzania poprawności certyfikatu SSL hello |
   | **443** | Cała komunikacja wychodząca naszej usługi |
   
   Jeśli Zapora wymusza zasady zgodnie z toooriginating użytkowników, należy otworzyć te porty dla ruchu z usług systemu Windows, które działają jako usługa sieciowa.
   - Jeśli zapora lub serwer proxy zezwala na listę dozwolonych podobnej DNS, połączeń dozwolonych zbyt**\*. msappproxy.net** i  **\*. servicebus.windows.net**. Jeśli nie, Zezwalaj na dostęp za[zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653), która jest aktualizowana co tydzień.
   - Agentów uwierzytelniania wymagany dostęp zbyt**login.windows.net** i **login.microsoftonline.com** do pierwszej rejestracji dla tych adresów URL również Otwórz zaporę.
   - Do weryfikacji certyfikatu odblokować hello następujące adresy URL: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** i  **www.microsoft.com:80**. Te adresy URL są używane do weryfikacji certyfikatu z innymi produktami firmy Microsoft, może już istnieć tych adresów URL odblokowany.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Krok 2: Włącz obsługę protokołu Exchange ActiveSync (opcjonalnie)

Wykonaj te instrukcje tooenable obsługę programu Exchange ActiveSync:

1. Użyj [środowiska PowerShell usługi Exchange](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) hello toorun następujące polecenie:
```
Get-OrganizationConfig | fl per*
```

2. Sprawdź wartość hello hello `PerTenantSwitchToESTSEnabled` ustawienie. Jeśli wartość hello jest **true**, dzierżawy jest prawidłowo skonfigurowana — zwykle jest to hello w przypadku większości klientów. Jeśli wartość hello jest **false**Uruchom hello następujące polecenie:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Sprawdź, czy hello z hello `PerTenantSwitchToESTSEnabled` jest teraz ustawienie zbyt**true**. Zaczekaj godzinę przed przenoszenie toohello następnego kroku.

Jeśli w tym kroku stają przed wszelkie problemy, sprawdź naszych [przewodnik rozwiązywania problemów](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) Aby uzyskać więcej informacji.

## <a name="step-3-enable-hello-feature"></a>Krok 3: Włączanie funkcji hello

Uwierzytelniania przekazywanego można włączyć za pomocą [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Na serwerze podstawowej lub tymczasowej Connect hello Azure AD można włączyć uwierzytelniania przekazywanego. Zdecydowanie zaleca się włączenie z serwera podstawowego hello.

Jeśli instalujesz Azure AD Connect na powitania po raz pierwszy, wybierz hello [niestandardową ścieżkę](active-directory-aadconnect-get-started-custom.md). Na powitania **logowania użytkownika** wybierz pozycję **uwierzytelniania przekazywanego** jako hello logowania dla metody. Po pomyślnym ukończeniu na powitania jest zainstalowany agent programu uwierzytelniania przekazywanego tym samym serwerze co usługi Azure AD Connect. Ponadto funkcja uwierzytelniania przekazywanego hello jest włączona w dzierżawie.

![Azure AD Connect - logowanie użytkowników](./media/active-directory-aadconnect-sso/sso3.png)

Jeśli użytkownik zainstalował już Azure AD Connect (przy użyciu hello [instalacji ekspresowej](active-directory-aadconnect-get-started-express.md) lub hello [instalacji niestandardowej](active-directory-aadconnect-get-started-custom.md) ścieżki) wybierz pozycję **strony logowania użytkownika zmiany** w usłudze Azure AD Połącz, a następnie kliknij pozycję **dalej**. Następnie wybierz **uwierzytelniania przekazywanego** jako hello logowania dla metody. Po pomyślnym ukończeniu na powitania jest zainstalowany agent programu uwierzytelniania przekazywanego tym samym serwerze co usługi Azure AD Connect i hello funkcja jest włączona na dzierżawy.

![Azure AD Connect - zmiany logowania użytkownika](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>Przekazywanego uwierzytelniania jest funkcją poziomie dzierżawy. Włączenie ma wpływ na logowanie użytkowników między _wszystkie_ hello zarządzane domeny w dzierżawie. Przy przejściu z tooPass do uwierzytelniania usług AD FS, firma Microsoft zaleca, aby poczekać co najmniej 12 godzin przed zamknięciem infrastruktury usług AD FS — czas oczekiwania jest tooensure, które użytkownicy mogą przechowywać logowanie tooExchange ActiveSync podczas przejścia.

## <a name="step-4-test-hello-feature"></a>Krok 4: Testowanie hello funkcji

Wykonaj te instrukcje tooverify, prawidłowo włączona przekazywanego uwierzytelniania:

1. Zaloguj się toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) z hello poświadczenia administratora globalnego dla dzierżawy.
2. Wybierz **usługi Azure Active Directory** na powitania nawigacji po lewej stronie.
3. Wybierz **programu Azure AD Connect**.
4. Sprawdź, że hello **uwierzytelniania przekazywanego** funkcji jest pokazywana jako **włączone**.
5. Wybierz **uwierzytelniania przekazywanego**. Ten blok Wyświetla listę serwerów hello, w których zainstalowano agentów uwierzytelniania.

![Centrum administracyjne usługi Azure Active Directory — blok Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centrum administracyjne usługi Active Directory platformy Azure — blok przekazywanego uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

Na tym etapie użytkowników ze wszystkich domen zarządzanych w Twojej dzierżawie zalogować się przy użyciu uwierzytelniania przekazywanego. Jednak użytkownicy z domen federacyjnych nadal toosign przy użyciu usługi Active Directory Federation Services (AD FS) lub innego dostawcy federacyjnego, który został wcześniej skonfigurowany. Po skonwertowaniu domeny z toomanaged federacyjnych, wszyscy użytkownicy z tej domeny automatyczne uruchamianie, logowanie przy użyciu uwierzytelniania przekazywanego. Funkcji uwierzytelniania przekazywanego hello nie wpływa na użytkowników tylko w chmurze.

## <a name="step-5-ensure-high-availability"></a>Krok 5: Zapewni to wysoką dostępność

Jeśli planujesz toodeploy uwierzytelniania przekazywanego w środowisku produkcyjnym, należy zainstalować autonomiczny Agent uwierzytelniania. Zainstaluj agenta tego drugiego uwierzytelniania na serwerze _innych_ niż hello jednym systemem Azure AD Connect i hello pierwszego uwierzytelniania agenta. Ta konfiguracja zapewnia wysoką dostępność żądań logowania. Wykonaj te instrukcje toodeploy autonomiczny Agent uwierzytelniania:

1. **Pobieranie najnowszej wersji hello hello Agent uwierzytelniania (wersje 1.5.193.0 lub nowszym)**: Zaloguj toohello [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com) przy użyciu poświadczeń administratora globalnego Twojej dzierżawy.
2. Wybierz **usługi Azure Active Directory** na powitania nawigacji po lewej stronie.
3. Wybierz **programu Azure AD Connect** , a następnie **uwierzytelniania przekazywanego**. I wybierz **pobierania agenta**.
4. Kliknij przycisk hello **zaakceptować & pobieranie** przycisku.
5. **Zainstaluj najnowszą wersję hello Agent uwierzytelniania hello**: hello uruchomienia pliku wykonywalnego pobranego w hello poprzedzających krok. Podaj poświadczenia administratora globalnego Twojej dzierżawy, po wyświetleniu monitu.

![Centrum administracyjne usługi Active Directory platformy Azure — przycisk Pobierz agenta uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Centrum administracyjne usługi Active Directory platformy Azure — Pobierz agenta bloku](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>Możesz również pobrać hello Agent uwierzytelniania z [tutaj](https://aka.ms/getauthagent). Sprawdź, czy Przejrzyj i zaakceptuj Agent uwierzytelniania hello [warunki świadczenia usługi](https://aka.ms/authagenteula) _przed_ instalacji.

## <a name="next-steps"></a>Następne kroki
- [**Bieżące ograniczenia** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — ta funkcja jest obecnie w przeglądzie. Dowiedz się, jakie scenariusze są obsługiwane i zostały.
- [**Nowości techniczne** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
