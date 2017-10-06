---
title: "Azure AD Connect: Rozwiązywanie problemów z bezproblemowe logowanie jednokrotne | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób tootroubleshoot Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne)."
services: active-directory
keywords: "Co to jest usługa Azure AD Connect, zainstaluj usługę Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Rozwiązywanie problemów z usługi Azure Active Directory bezproblemowe logowanie jednokrotne

Ten artykuł pomaga informacje o typowych problemów dotyczących usługi Azure AD bezproblemowe logowanie jednokrotne.

## <a name="known-issues"></a>Znane problemy

- Jeśli planowana jest synchronizacja 30 lub większą liczbą lasów usługi AD, nie można włączyć bezproblemowe logowanie Jednokrotne za pomocą usługi Azure AD Connect. Jako rozwiązanie alternatywne można [ręcznie włączyć](#manual-reset-of-azure-ad-seamless-sso) funkcję hello w dzierżawie.
- Dodawanie usługi Azure AD service adresów URL (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello "strefy Zaufane witryny" zamiast strefy "Lokalny intranet" hello **uniemożliwia użytkownikom logowanie**.
- Bezproblemowe logowanie Jednokrotne nie działa w trybie przeglądania prywatnym Firefox i krawędzi. I również w programie Internet Explorer po włączeniu trybu ochrony rozszerzone.

>[!IMPORTANT]
>Firma Microsoft niedawno wycofane obsługę tooinvestigate krawędzi problemy zgłoszone przez klienta.

## <a name="check-status-of-hello-feature"></a>Sprawdź stan hello funkcji

Upewnij się, ta funkcja logowania jednokrotnego bezproblemowe hello jest nadal **włączone** w dzierżawie. Stan można sprawdzić przez przejście toohello **Azure AD Connect** bloku na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/).

![Centrum administracyjne usługi Azure Active Directory — blok Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Przyczyny niepowodzenia logowania w Centrum administracyjnym usługi Active Directory Azure hello

Toostart dobrym miejscem problemów użytkownika logowania z bezproblemowe rejestracji Jednokrotnej jest toolook na powitania [raport aktywności logowania](../active-directory-reporting-activity-sign-ins.md) na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/).

![Centrum administracyjne usługi Active Directory platformy Azure — raport logowania](./media/active-directory-aadconnect-sso/sso9.png)

Przejdź za**usługi Azure Active Directory** -> **logowania** na powitania [Centrum administracyjnego usługi Azure Active Directory](https://aad.portal.azure.com/) i kliknij przycisk działań logowania określonego użytkownika. Wyszukaj hello **kod błędu logowania w** pola. Mapowanie wartości hello tego przyczyna niepowodzenia tooa pola i rozpoznawanie przy użyciu hello w poniższej tabeli:

|Kod błędu logowania|Przyczyna niepowodzenia logowania|Rozwiązanie
| --- | --- | ---
| 81001 | Bilet Kerberos użytkownika jest zbyt duży. | Zmniejsz członkostwa grupy użytkownika i spróbuj ponownie.
| 81002 | Użytkownik toovalidate biletu Kerberos. | Zobacz [Rozwiązywanie problemów z listy kontrolnej](#troubleshooting-checklist).
| 81003 | Użytkownik toovalidate biletu Kerberos. | Zobacz [Rozwiązywanie problemów z listy kontrolnej](#troubleshooting-checklist).
| 81004 | Próba uwierzytelniania Kerberos nie powiodła się. | Zobacz [Rozwiązywanie problemów z listy kontrolnej](#troubleshooting-checklist).
| 81008 | Użytkownik toovalidate biletu Kerberos. | Zobacz [Rozwiązywanie problemów z listy kontrolnej](#troubleshooting-checklist).
| 81009 | "Biletu Kerberos toovalidate użytkownika. | Zobacz [Rozwiązywanie problemów z listy kontrolnej](#troubleshooting-checklist).
| 81010 | Bezproblemowe logowanie Jednokrotne nie powiodło się, ponieważ biletu Kerberos hello użytkownika wygasło lub jest nieprawidłowy. | Użytkownik musi toosign w urządzeniu przyłączonym do domeny w sieci firmowej.
| 81011 | Obiekt użytkownika toofind na podstawie informacji biletu Kerberos hello użytkownika. | Użyj usługi Azure AD Connect toosynchronize informacje o użytkowniku w usłudze Azure Active Directory.
| 81012 | Hello użytkownika w trakcie toosign w tooAzure AD różni się od użytkownika hello w urządzeniu hello zalogowany. | Zaloguj się z innego urządzenia.
| 81013 | Obiekt użytkownika toofind na podstawie informacji biletu Kerberos hello użytkownika. |Użyj usługi Azure AD Connect toosynchronize informacje o użytkowniku w usłudze Azure Active Directory. 

## <a name="troubleshooting-checklist"></a>Rozwiązywanie problemów z listy kontrolnej

Użyj hello następujące problemy bezproblemowe logowanie Jednokrotne tootroubleshoot Lista kontrolna:

- Sprawdź, czy funkcja logowania jednokrotnego bezproblemowe hello jest włączona w programie Azure AD Connect. Jeśli nie można włączyć funkcję hello (na przykład ze względu tooa zablokowany port), upewnij się, że masz wszystkie hello [wstępne](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) w miejscu.
- Sprawdź, czy obie te usługi Azure AD adresy URL (https://autologon.microsoftazuread-sso.com i https://aadg.windows.net.nsatc.net) są częścią ustawienia strefy Intranet hello użytkownika.
- Upewnij się, że urządzeń firmowych hello jest przyłączony do toohello AD domeny.
- Upewnij się, że hello użytkownik jest zalogowany przy użyciu konta domeny AD urządzenia toohello.
- Upewnij się, że konto użytkownika hello w lesie usługi AD, w którym zostało bezproblemowe logowanie Jednokrotne skonfigurowano.
- Upewnij się, że hello urządzenie jest połączone hello w sieci firmowej.
- Upewnij się, że godzina na urządzeniu hello jest zsynchronizowany z czasem hello Active Directory i kontrolery domeny hello i jest w ciągu pięciu minut od siebie.
- Wyświetl listę istniejących biletów Kerberos na urządzeniu hello hello **klist** polecenia z wiersza polecenia. Sprawdź, jeśli bilety wystawione dla hello `AZUREADSSOACCT` istnieją konta komputera. Bilety Kerberos użytkowników są zazwyczaj prawidłowe 12 godzin. W usłudze Active Directory, może mieć różne ustawienia.
- Przeczyszczenia istniejące bilety Kerberos hello urządzenia przy użyciu hello **przeczyścić klist** polecenia, a następnie spróbuj ponownie.
- toodetermine, jeśli występują problemy związane z JavaScript, przejrzyj dzienniki konsoli hello hello przeglądarki (w obszarze "Developer Tools").
- Przejrzyj hello [kontroler domeny](#domain-controller-logs) również.

### <a name="domain-controller-logs"></a>Kontroler domeny

Jeśli inspekcja sukcesów jest włączona na kontrolerze domeny, następnie za każdym razem, gdy użytkownik loguje się przy użyciu łatwego logowania jednokrotnego zapisu zabezpieczeń jest rejestrowany w dzienniku zdarzeń hello. Można znaleźć tych zdarzeń zabezpieczeń za pomocą następującej kwerendy hello (Znajdź zdarzenie **4769** skojarzone z kontem komputera hello **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Resetowanie ręczne hello funkcji

Jeśli rozwiązywania problemów nie pomogły, można ręcznie zresetować funkcji hello w dzierżawie. Wykonaj następujące kroki na powitania serwera lokalnego, na którym uruchomiony jest program Azure AD Connect:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>: Krok 1 moduł bezproblemowe PowerShell logowania jednokrotnego hello

1. Najpierw należy pobrać i zainstalować hello [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Następnie Pobierz i zainstaluj hello [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Przejdź toohello `%programfiles%\Microsoft Azure Active Directory Connect` folderu.
4. Moduł bezproblemowe PowerShell logowania jednokrotnego hello importu za pomocą tego polecenia: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Krok 2: Pobieranie listy hello lasów usługi AD, dla których włączono bezproblemowe logowanie Jednokrotne

1. Uruchom program PowerShell jako Administrator. W programie PowerShell, wywołaj `New-AzureADSSOAuthenticationContext`. Po wyświetleniu monitu wprowadź poświadczenia administratora globalnego Twojej dzierżawy.
2. Wywołanie `Get-AzureADSSOStatus`. Tego polecenia zapewnia hello listy lasów usługi AD (zobacz listę domen"hello"), na którym ta funkcja została włączona.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Krok 3: Wyłącz bezproblemowe logowanie Jednokrotne dla każdego lasu usługi AD, skonfigurowanego go go na

1. Wywołanie `$creds = Get-Credential`. Po wyświetleniu monitu wprowadź poświadczenia administratora domeny hello na powitania przeznaczone lesie usługi Active Directory.
2. Wywołanie `Disable-AzureADSSOForest -OnPremCredentials $creds`. To polecenie usuwa hello `AZUREADSSOACCT` konto komputera z hello lokalnego kontrolera domeny dla tego określonego lasu usługi AD.
3. Powtórz hello w poprzednich krokach dla każdego lasu usługi AD, która po skonfigurowaniu funkcji hello na.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Krok 4: Włącz bezproblemowe logowanie Jednokrotne dla każdego lasu usługi AD

1. Wywołanie `Enable-AzureADSSOForest`. Po wyświetleniu monitu wprowadź poświadczenia administratora domeny hello na powitania przeznaczone lesie usługi Active Directory.
2. Powtórz hello w poprzednich krokach dla każdego lasu usługi AD, który ma tooset funkcji hello na.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Krok 5. Włącz funkcję hello na dzierżawy

Wywołanie `Enable-AzureADSSO` i wprowadź wartość "true" w hello `Enable: ` monitu tooturn funkcję hello w dzierżawie.
