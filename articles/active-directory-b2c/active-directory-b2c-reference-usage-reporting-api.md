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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="82d81-103">Uzyskiwanie dostępu do raportów użycia w usłudze Azure AD B2C za pośrednictwem hello raportowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="82d81-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="82d81-104">Usługa Azure Active Directory B2C (Azure AD B2C) zapewnia uwierzytelnianie na podstawie użytkownika, logowanie i uwierzytelnianie wieloskładnikowe Azure.</span><span class="sxs-lookup"><span data-stu-id="82d81-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="82d81-105">Uwierzytelnianie jest dostępna dla użytkowników końcowych rodziny aplikacji przez dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="82d81-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="82d81-106">Znając hello liczbę użytkowników zarejestrowanych w dzierżawie powitalnych, dostawców hello używały tooregister i hello liczbę uwierzytelnień według typu, pozwala odpowiedzieć na pytania, takich jak:</span><span class="sxs-lookup"><span data-stu-id="82d81-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="82d81-107">Ilu użytkowników z każdego typu dostawcy tożsamości (na przykład konto Microsoft lub LinkedIn) zostały zarejestrowane w hello ostatnich 10 dni?</span><span class="sxs-lookup"><span data-stu-id="82d81-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="82d81-108">Ile uwierzytelnienia przy użyciu usługi Multi-Factor Authentication zostały ukończone pomyślnie w hello ostatnim miesiącu?</span><span class="sxs-lookup"><span data-stu-id="82d81-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="82d81-109">Ile uwierzytelnienia logowania w podstawie zostały ukończone w tym miesiącu?</span><span class="sxs-lookup"><span data-stu-id="82d81-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="82d81-110">Dziennie?</span><span class="sxs-lookup"><span data-stu-id="82d81-110">Per day?</span></span> <span data-ttu-id="82d81-111">Na aplikację?</span><span class="sxs-lookup"><span data-stu-id="82d81-111">Per application?</span></span>
* <span data-ttu-id="82d81-112">Jak można oszacować się, że hello oczekiwano miesięczny koszt działania dzierżawy usługi Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="82d81-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="82d81-113">Ten artykuł skupia się na działalność toobilling powiązane raporty, która jest oparta na hello liczbę użytkowników, rozliczeniowy Zaloguj się w podstawie uwierzytelnienia i uwierzytelnienia wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="82d81-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="82d81-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="82d81-114">Prerequisites</span></span>
<span data-ttu-id="82d81-115">Przed rozpoczęciem pracy należy kroki hello toocomplete [hello tooaccess wymagania wstępne dotyczące raportowania usługi Azure AD interfejsów API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="82d81-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="82d81-116">Tworzenie aplikacji, uzyskać klucz tajny i raporty dzierżawy usługi Azure AD B2C tooyour praw grant mieć do niej dostęp.</span><span class="sxs-lookup"><span data-stu-id="82d81-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="82d81-117">*Bash skryptu* i *skrypt w języku Python* zamieszczono przykłady, które również w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="82d81-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="82d81-118">Skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="82d81-118">PowerShell script</span></span>
<span data-ttu-id="82d81-119">Ten skrypt pokazuje hello tworzenia raportów użycia czterech przy użyciu hello `TimeStamp` parametr i hello `ApplicationId` filtru.</span><span class="sxs-lookup"><span data-stu-id="82d81-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

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


## <a name="usage-report-definitions"></a><span data-ttu-id="82d81-120">Definicje raportów użycia</span><span class="sxs-lookup"><span data-stu-id="82d81-120">Usage report definitions</span></span>
* <span data-ttu-id="82d81-121">**tenantUserCount**: hello liczbę użytkowników w dzierżawie powitalnych według typu dostawcy tożsamości, dziennie w hello ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="82d81-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="82d81-122">(Opcjonalnie `TimeStamp` filtru zawiera liczby użytkowników z toohello określona data bieżąca data).</span><span class="sxs-lookup"><span data-stu-id="82d81-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="82d81-123">Raport Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="82d81-123">hello report provides:</span></span>
  * <span data-ttu-id="82d81-124">**TotalUserCount**: hello liczbę wszystkich obiektów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="82d81-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="82d81-125">**OtherUserCount**: hello liczbę użytkowników usługi Azure Active Directory (nie użytkowników usługi Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="82d81-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="82d81-126">**LocalUserCount**: hello numer konta użytkownika usługi Azure AD B2C utworzone przy użyciu poświadczeń lokalnego toohello usługi Azure AD B2C dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="82d81-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="82d81-127">**AlternateIdUserCount**: hello liczbę użytkowników usługi Azure AD B2C zarejestrowane przy pomocy dostawcy tożsamości zewnętrznych (na przykład, Facebook, konta Microsoft lub innej dzierżawy usługi Azure Active Directory, nazywana także tooas `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="82d81-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="82d81-128">**b2cAuthenticationCountSummary**: Podsumowanie hello codzienne numer rozliczeniowy uwierzytelnienia za pośrednictwem hello ostatnich 30 dni, dzień, a typ Przepływ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="82d81-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="82d81-129">**b2cAuthenticationCount**: hello liczbę uwierzytelnień w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="82d81-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="82d81-130">domyślne Hello jest hello ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="82d81-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="82d81-131">(Opcjonalne: hello otwierające i zamykające `TimeStamp` parametry definiują okres określony czas.) zawiera dane wyjściowe hello `StartTimeStamp` (najwcześniejsza data działania dla tej dzierżawy) i `EndTimeStamp` (najnowsza aktualizacja).</span><span class="sxs-lookup"><span data-stu-id="82d81-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="82d81-132">**b2cMfaRequestCountSummary**: podsumowanie liczby hello codzienne operacje uwierzytelniania wieloskładnikowego, dzień, a typ (SMS lub głosowych).</span><span class="sxs-lookup"><span data-stu-id="82d81-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="82d81-133">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="82d81-133">Limitations</span></span>
<span data-ttu-id="82d81-134">Użytkownik liczba dane są odświeżane co 24 godziny too48.</span><span class="sxs-lookup"><span data-stu-id="82d81-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="82d81-135">Uwierzytelnienia są aktualizowane kilka razy dziennie.</span><span class="sxs-lookup"><span data-stu-id="82d81-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="82d81-136">Korzystając z hello `ApplicationId` filtr, odpowiedzi pusty raport może być z powodu tooone następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="82d81-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="82d81-137">Identyfikator aplikacji Hello nie istnieje w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="82d81-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="82d81-138">Upewnij się, że jest poprawny.</span><span class="sxs-lookup"><span data-stu-id="82d81-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="82d81-139">Identyfikator aplikacji Hello istnieje, ale nie znaleziono danych w hello okresu raportowania.</span><span class="sxs-lookup"><span data-stu-id="82d81-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="82d81-140">Przejrzyj parametry daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="82d81-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82d81-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82d81-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="82d81-142">Rachunek miesięczny szacuje dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="82d81-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="82d81-143">W połączeniu z [hello najnowsze usługi Azure AD B2C cennik dostępne](https://azure.microsoft.com/pricing/details/active-directory-b2c/), można oszacować dzienne, tygodniowe i miesięczne wykorzystania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="82d81-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="82d81-144">Szacowana jest szczególnie przydatne podczas planowania zmiany w zachowaniu dzierżawy, który może mieć wpływ na całkowity koszt.</span><span class="sxs-lookup"><span data-stu-id="82d81-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="82d81-145">Możesz przejrzeć koszty rzeczywiste w Twojej [połączonej subskrypcji Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="82d81-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="82d81-146">Opcje dla innych formatów wyjściowych</span><span class="sxs-lookup"><span data-stu-id="82d81-146">Options for other output formats</span></span>
<span data-ttu-id="82d81-147">Witaj poniższy kod przedstawia przykłady wysyłania danych wyjściowych tooJSON, listy wartości nazw i XML:</span><span class="sxs-lookup"><span data-stu-id="82d81-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
