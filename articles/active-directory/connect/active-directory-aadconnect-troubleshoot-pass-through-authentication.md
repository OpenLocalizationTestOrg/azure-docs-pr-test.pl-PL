---
title: "Azure AD Connect: Rozwiązywanie problemów z uwierzytelniania przekazywanego | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tootroubleshoot uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Rozwiązywanie problemów z usługi Azure AD Connect uwierzytelniania przekazywanego, należy zainstalować usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Rozwiązywanie problemów z uwierzytelniania przekazywanego usługi Azure Active Directory

Ten artykuł pomaga informacje o typowych problemów dotyczących usługi Azure AD przekazywanego uwierzytelniania.

>[!IMPORTANT]
>Jeśli są ukierunkowane użytkownika logowania problemów przy użyciu uwierzytelniania przekazywanego, nie wyłączyć funkcję hello lub odinstalować agentów uwierzytelniania przekazywanego bez konieczności ponownego tylko w chmurze toofall konta administratora globalnego. Dowiedz się więcej o [dodanie konta administratora globalnego tylko w chmurze](../active-directory-users-create-azure-portal.md). Wykonanie tego kroku jest krytyczna i zapewnia, że należy przed zablokowaniem dzierżawy.

## <a name="general-issues"></a>Ogólne problemy

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Sprawdź stan funkcji hello i uwierzytelniania agentów

Upewnij się, ta funkcja uwierzytelniania przekazywanego hello jest nadal **włączone** na Twojej dzierżawy i hello stan agentów uwierzytelniania wyświetlany **Active**i nie **nieaktywne**. Stan można sprawdzić przez przejście toohello **Azure AD Connect** bloku na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/).

![Centrum administracyjne usługi Azure Active Directory — blok Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Centrum administracyjne usługi Active Directory platformy Azure — blok przekazywanego uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Błąd logowania dla użytkownika wiadomości

Jeśli użytkownik hello jest toosign do przy użyciu przekazywanego uwierzytelniania, ich może zostać wyświetlony jeden z hello następujące błędy dla użytkownika na ekranie logowania hello Azure AD: 

|Błąd|Opis|Rozwiązanie
| --- | --- | ---
|AADSTS80001|Nie można tooconnect tooActive katalogu|Sprawdź, czy agent serwery są elementami członkowskimi hello AD tego samego lasu jako hello użytkowników, których hasła muszą toobe zweryfikowane i są one możliwe tooconnect tooActive katalogu.  
|AADSTS8002|Upłynął limit czasu połączenia tooActive katalogu|Sprawdź tooensure, że usługi Active Directory jest dostępny i odpowiada toorequests z hello agentów.
|AADSTS80004|username Hello przekazywane agenta toohello jest nieprawidłowa|Upewnij się, że hello użytkownik próbuje toosign się przy użyciu hello prawo nazwy użytkownika.
|AADSTS80005|Sprawdzanie poprawności napotkano nieprzewidywalne WebException|Błąd przejściowy. Ponów żądanie hello. Jeśli nadal toofail, skontaktuj się z pomocą techniczną firmy Microsoft.
|AADSTS80007|Wystąpił błąd podczas komunikacji z usługą Active Directory|Sprawdź dzienniki agenta hello, aby uzyskać więcej informacji i sprawdź, czy usługi Active Directory działa zgodnie z oczekiwaniami.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Przyczyny niepowodzenia logowania w Centrum administracyjnym usługi Active Directory Azure hello

Uruchamianie rozwiązywania problemów problemy z logowaniem użytkownika, analizując hello [raport aktywności logowania](../active-directory-reporting-activity-sign-ins.md) na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/).

![Centrum administracyjne usługi Active Directory platformy Azure — raport logowania](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Przejdź za**usługi Azure Active Directory** -> **logowania** na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/) i kliknij przycisk działań logowania określonego użytkownika. Wyszukaj hello **kod błędu logowania w** pola. Mapowanie wartości hello tego przyczyna niepowodzenia tooa pola i rozpoznawanie przy użyciu hello w poniższej tabeli:

|Kod błędu logowania|Przyczyna niepowodzenia logowania|Rozwiązanie
| --- | --- | ---
| 50144 | Ważność hasła użytkownika usługi Active Directory wygasła. | Zresetowanie hasła użytkownika hello w lokalnej usługi Active Directory.
| 80001 | Brak dostępnych agentów uwierzytelniania. | Zainstaluj i zarejestruj Agent uwierzytelniania.
| 80002 | Upłynął limit czasu żądania weryfikacji hasła agenta uwierzytelniania. | Sprawdź, czy usługi Active Directory jest dostępny z hello Agent uwierzytelniania.
| 80003 | Agent uwierzytelniania odebrał nieprawidłową odpowiedź. | Jeśli hello problem się stale powtarza przez wielu użytkowników, sprawdź konfigurację usługi Active Directory.
| 80004 | W żądaniu logowania użyto nieprawidłowej głównej nazwy użytkownika (UPN). | Poproś hello toosign użytkownika za pomocą hello prawidłową nazwę użytkownika.
| 80005 | Agent uwierzytelniania: wystąpił błąd. | Błąd przejściowy. Spróbuj ponownie później.
| 80007 | Uwierzytelnianie agenta tooconnect tooActive katalogu. | Sprawdź, czy usługi Active Directory jest dostępny z hello Agent uwierzytelniania.
| 80010 | Hasło toodecrypt Agent uwierzytelniania. | Jeśli hello problem się stale powtarza, zainstaluj i Zarejestruj nowy Agent uwierzytelniania. I Odinstaluj hello bieżący. 
| 80011 | Klucz odszyfrowujący tooretrieve Agent uwierzytelniania. | Jeśli hello problem się stale powtarza, zainstaluj i Zarejestruj nowy Agent uwierzytelniania. I Odinstaluj hello bieżący.

## <a name="authentication-agent-installation-issues"></a>Problemy z instalacją agentów uwierzytelniania

### <a name="an-unexpected-error-occurred"></a>Wystąpił nieoczekiwany błąd

[Zbieranie dzienników agenta](#collecting-pass-through-authentication-agent-logs) hello server i skontaktuj się z Microsoft Support w rozwiązaniu problemu.

## <a name="authentication-agent-registration-issues"></a>Problemy z uwierzytelnianiem agenta rejestracji

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Rejestracja hello uwierzytelniania agenta nie powiodła z powodu tooblocked portów

Upewnij się, ten serwer hello, na które hello jest zainstalowany Agent uwierzytelniania może komunikować się z naszej usługi adresów URL i portów wyświetlane [tutaj](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Rejestracja hello uwierzytelniania agenta nie powiodła z powodu błędów autoryzacji tootoken lub konta

Upewnij się, użyj konta administratora globalnego tylko w chmurze Azure AD Connect lub autonomicznej Agent uwierzytelniania i operacji rejestracji. Jest to znany problem z konta administratora globalnego włączone uwierzytelnianie MFA; Wyłącz funkcję MFA tymczasowo (tylko operacje hello toocomplete) jako obejście.

### <a name="an-unexpected-error-occurred"></a>Wystąpił nieoczekiwany błąd

[Zbieranie dzienników agenta](#collecting-pass-through-authentication-agent-logs) hello server i skontaktuj się z Microsoft Support w rozwiązaniu problemu.

## <a name="authentication-agent-uninstallation-issues"></a>Problemy z uwierzytelnianiem agenta dezinstalacji

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Ostrzeżenie podczas odinstalowywania Azure AD Connect

Jeśli masz uwierzytelniania przekazywanego włączone dzierżawy i spróbuj toouninstall Azure AD Connect, pokazuje hello następujące ostrzeżenie: "użytkownicy nie będą mogli toosign w tooAzure AD w przypadku braku innych agentów przekazywania uwierzytelniania zainstalowane na innych serwerach."

Upewnij się, że ustawienia są [wysokiej dostępności](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) przed odinstalowaniem tooavoid Azure AD Connect fundamentalne logowania użytkownika.

## <a name="issues-with-enabling-hello-feature"></a>Problemy z włączaniem hello funkcji

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Włączenie funkcji hello nie powiodło się, ponieważ nie było żadnych agentów uwierzytelniania

Należy toohave co najmniej jeden aktywny Agent uwierzytelniania tooenable uwierzytelniania przekazywanego w dzierżawie. Można zainstalować agenta uwierzytelniania przez zainstalowanie usługi Azure AD Connect lub autonomiczny Agent uwierzytelniania.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Włączenie funkcji hello nie powiodła z powodu tooblocked portów

Upewnij się, ten serwer hello, na którym zainstalowano Azure AD Connect może komunikować się z usługą adresów URL i portów wyświetlane [tutaj](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Włączenie funkcji hello nie powiodła z powodu błędów autoryzacji tootoken lub konta

Upewnij się, że używasz konta administratora globalnego tylko w chmurze, podczas włączania funkcji hello. Jest to znany problem z uwierzytelnianiem wieloskładnikowym (MFA)-włączone konta administratora globalnego; Wyłącz funkcję MFA tymczasowo (tylko operacja hello toocomplete) jako obejście.

## <a name="exchange-activesync-configuration-issues"></a>Problemy z konfiguracją programu Exchange ActiveSync

Po skonfigurowaniu programu Exchange ActiveSync obsługę uwierzytelniania przekazywanego są hello typowych problemów.

### <a name="exchange-powershell-issue"></a>Problem PowerShell programu Exchange

Jeśli widzisz hello "**nie można odnaleźć parametru odpowiadającej nazwie parametru"PerTenantSwitchToESTSEnabled"\.**" Błąd podczas uruchamiania hello `Set-OrganizationConfig` środowiska PowerShell usługi Exchange polecenie, skontaktuj się z Microsoft Support.

### <a name="exchange-activesync-not-working"></a>Program Exchange ActiveSync nie działa

Konfiguracja Hello obowiązuje niektórych czas tootake — hello okres czasu w zależności od środowiska. Jeśli sytuacja hello będzie nadal występować przez długi czas, skontaktuj się z Microsoft Support.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Zbieranie dzienników przekazywanego uwierzytelniania agenta

W zależności od typu hello problemu, który może być konieczne toolook w różnych miejscach dzienników Agent uwierzytelniania przekazywanego.

### <a name="authentication-agent-event-logs"></a>Dzienniki zdarzeń uwierzytelniania agenta

Błędy związane z toohello Agent uwierzytelniania, otwarcie hello podglądu zdarzeń aplikacji na powitania serwera i sprawdź w obszarze **aplikacji i usług Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Szczegółowe analizy Włącz dziennik "Session" hello. Nie uruchamiaj hello Agent uwierzytelniania z tym dziennikiem włączona podczas wykonywania normalnych operacji; używana tylko w celu rozwiązania problemu. zawartość dziennika Hello są widoczne tylko po wyłączeniu dziennika hello ponownie.

### <a name="detailed-trace-logs"></a>Dzienniki śledzenia szczegółowe

Użytkownik tootroubleshoot błędów logowania Wyszukaj dzienniki śledzenia w **%programdata%\Microsoft\Azure AD Connect Agent\Trace uwierzytelniania\\**. Dzienniki te obejmują przyczyny logowania użytkownika określonych niepowodzeń przy użyciu funkcji uwierzytelniania przekazywanego hello. Te błędy są również podanych w poprzednim hello przyczyn błąd logowania mapowanego toohello [tabeli](#sign-in-failure-reasons-on-the-Azure-portal). Poniżej przedstawiono przykładowy wpis dziennika:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

Opisową informacji hello błędu ("1328" w hello poprzedzających przykład) można uzyskać, otwierając hello wiersza polecenia i uruchomione hello następujące polecenie (Uwaga: Zamień "1328" numer błędu hello, które pojawi się w dziennikach):

`Net helpmsg 1328`

![Uwierzytelnianie przekazywane](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Kontroler domeny

Jeśli włączono rejestrowanie inspekcji, dodatkowe informacje można znaleźć w hello dzienniki zabezpieczeń kontrolerów domeny. Prosty sposób tooquery logowania żądania wysyłane przez agentów uwierzytelniania przekazywanego wygląda następująco:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Liczniki Monitora wydajności

Inny sposób toomonitor agentów uwierzytelniania jest liczniki Monitora wydajności dotyczące tootrack na każdym serwerze, na którym zainstalowano hello Agent uwierzytelniania. Użyj hello następujące liczniki globalne (**uwierzytelnienia # PTA**, **#PTA uwierzytelnianie nie powiodło się** i **#PTA informacji o pomyślnym uwierzytelnieniu**) i liczniki błędu (**Błędy uwierzytelniania # PTA**):

![Liczniki Monitora wydajności uwierzytelniania przekazywanego](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>Uwierzytelniania przekazywanego zapewnia wysoką dostępność, za pomocą wielu agentów uwierzytelniania, i _nie_ Równoważenie obciążenia. W zależności od konfiguracji _nie_ wszystkich agentów uwierzytelniania odbierania około _równy_ liczby żądań. Możliwe jest określony Agent uwierzytelniania na wszystkich odbiera żaden ruch.
