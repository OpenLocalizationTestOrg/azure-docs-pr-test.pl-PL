---
title: "Usługa Azure Active Directory B2C: Przykłady interfejsu API raportowania użycia i definicje | Dokumentacja firmy Microsoft"
description: "Przewodnik i przykłady dotyczące konfigurowania raportów dzierżawcy usługi Azure AD B2C, użytkowników, uwierzytelnianie i operacje uwierzytelniania wieloskładnikowego"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Uzyskiwanie dostępu do raportów użycia w usłudze Azure AD B2C za pośrednictwem hello raportowania interfejsu API

Usługa Azure Active Directory B2C (Azure AD B2C) zapewnia uwierzytelnianie na podstawie użytkownika, logowanie i uwierzytelnianie wieloskładnikowe Azure. Uwierzytelnianie jest dostępna dla użytkowników końcowych rodziny aplikacji przez dostawców tożsamości. Znając hello liczbę użytkowników zarejestrowanych w dzierżawie powitalnych, dostawców hello używały tooregister i hello liczbę uwierzytelnień według typu, pozwala odpowiedzieć na pytania, takich jak:
* Ilu użytkowników z każdego typu dostawcy tożsamości (na przykład konto Microsoft lub LinkedIn) zostały zarejestrowane w hello ostatnich 10 dni?
* Ile uwierzytelnienia przy użyciu usługi Multi-Factor Authentication zostały ukończone pomyślnie w hello ostatnim miesiącu?
* Ile uwierzytelnienia logowania w podstawie zostały ukończone w tym miesiącu? Dziennie? Na aplikację?
* Jak można oszacować się, że hello oczekiwano miesięczny koszt działania dzierżawy usługi Azure AD B2C?

Ten artykuł skupia się na działalność toobilling powiązane raporty, która jest oparta na hello liczbę użytkowników, rozliczeniowy Zaloguj się w podstawie uwierzytelnienia i uwierzytelnienia wieloskładnikowego.


## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem pracy należy kroki hello toocomplete [hello tooaccess wymagania wstępne dotyczące raportowania usługi Azure AD interfejsów API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Tworzenie aplikacji, uzyskać klucz tajny i raporty dzierżawy usługi Azure AD B2C tooyour praw grant mieć do niej dostęp. *Bash skryptu* i *skrypt w języku Python* zamieszczono przykłady, które również w tym miejscu. 

## <a name="powershell-script"></a>Skrypt programu PowerShell
Ten skrypt pokazuje hello tworzenia raportów użycia czterech przy użyciu hello `TimeStamp` parametr i hello `ApplicationId` filtru.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>Definicje raportów użycia
* **tenantUserCount**: hello liczbę użytkowników w dzierżawie powitalnych według typu dostawcy tożsamości, dziennie w hello ostatnich 30 dni. (Opcjonalnie `TimeStamp` filtru zawiera liczby użytkowników z toohello określona data bieżąca data). Raport Hello zawiera:
  * **TotalUserCount**: hello liczbę wszystkich obiektów użytkowników.
  * **OtherUserCount**: hello liczbę użytkowników usługi Azure Active Directory (nie użytkowników usługi Azure AD B2C).
  * **LocalUserCount**: hello numer konta użytkownika usługi Azure AD B2C utworzone przy użyciu poświadczeń lokalnego toohello usługi Azure AD B2C dzierżawy.

* **AlternateIdUserCount**: hello liczbę użytkowników usługi Azure AD B2C zarejestrowane przy pomocy dostawcy tożsamości zewnętrznych (na przykład, Facebook, konta Microsoft lub innej dzierżawy usługi Azure Active Directory, nazywana także tooas `OrgId`).

* **b2cAuthenticationCountSummary**: Podsumowanie hello codzienne numer rozliczeniowy uwierzytelnienia za pośrednictwem hello ostatnich 30 dni, dzień, a typ Przepływ uwierzytelniania.

* **b2cAuthenticationCount**: hello liczbę uwierzytelnień w przedziale czasu. domyślne Hello jest hello ostatnich 30 dni.  (Opcjonalne: hello otwierające i zamykające `TimeStamp` parametry definiują okres określony czas.) zawiera dane wyjściowe hello `StartTimeStamp` (najwcześniejsza data działania dla tej dzierżawy) i `EndTimeStamp` (najnowsza aktualizacja).

* **b2cMfaRequestCountSummary**: podsumowanie liczby hello codzienne operacje uwierzytelniania wieloskładnikowego, dzień, a typ (SMS lub głosowych).


## <a name="limitations"></a>Ograniczenia
Użytkownik liczba dane są odświeżane co 24 godziny too48. Uwierzytelnienia są aktualizowane kilka razy dziennie. Korzystając z hello `ApplicationId` filtr, odpowiedzi pusty raport może być z powodu tooone następujące warunki:
  * Identyfikator aplikacji Hello nie istnieje w dzierżawie powitalnych. Upewnij się, że jest poprawny.
  * Identyfikator aplikacji Hello istnieje, ale nie znaleziono danych w hello okresu raportowania. Przejrzyj parametry daty/godziny.


## <a name="next-steps"></a>Następne kroki
### <a name="monthly-bill-estimates-for-azure-ad"></a>Rachunek miesięczny szacuje dla usługi Azure AD
W połączeniu z [hello najnowsze usługi Azure AD B2C cennik dostępne](https://azure.microsoft.com/pricing/details/active-directory-b2c/), można oszacować dzienne, tygodniowe i miesięczne wykorzystania platformy Azure.  Szacowana jest szczególnie przydatne podczas planowania zmiany w zachowaniu dzierżawy, który może mieć wpływ na całkowity koszt. Możesz przejrzeć koszty rzeczywiste w Twojej [połączonej subskrypcji Azure](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opcje dla innych formatów wyjściowych
Witaj poniższy kod przedstawia przykłady wysyłania danych wyjściowych tooJSON, listy wartości nazw i XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
