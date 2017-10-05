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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="be51d-103">Uzyskiwanie dostępu do raportów użycia w usłudze Azure AD B2C za pośrednictwem interfejsu API raportowania</span><span class="sxs-lookup"><span data-stu-id="be51d-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="be51d-104">Usługa Azure Active Directory B2C (Azure AD B2C) zapewnia uwierzytelnianie na podstawie użytkownika, logowanie i uwierzytelnianie wieloskładnikowe Azure.</span><span class="sxs-lookup"><span data-stu-id="be51d-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="be51d-105">Uwierzytelnianie jest dostępna dla użytkowników końcowych rodziny aplikacji przez dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="be51d-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="be51d-106">Gdy wiesz, liczbę użytkowników zarejestrowanych w dzierżawie, dostawców używanego do rejestrowania i liczbę uwierzytelnień według typu, pozwala odpowiedzieć na pytania, takich jak:</span><span class="sxs-lookup"><span data-stu-id="be51d-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="be51d-107">Ilu użytkowników z każdego typu dostawcy tożsamości (na przykład konto Microsoft lub LinkedIn) zostały zarejestrowane w ciągu ostatnich 10 dni?</span><span class="sxs-lookup"><span data-stu-id="be51d-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="be51d-108">Ile uwierzytelnienia przy użyciu usługi Multi-Factor Authentication została ukończona pomyślnie w ostatnim miesiącu?</span><span class="sxs-lookup"><span data-stu-id="be51d-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="be51d-109">Ile uwierzytelnienia logowania w podstawie zostały ukończone w tym miesiącu?</span><span class="sxs-lookup"><span data-stu-id="be51d-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="be51d-110">Dziennie?</span><span class="sxs-lookup"><span data-stu-id="be51d-110">Per day?</span></span> <span data-ttu-id="be51d-111">Na aplikację?</span><span class="sxs-lookup"><span data-stu-id="be51d-111">Per application?</span></span>
* <span data-ttu-id="be51d-112">Jak można oszacować oczekiwanego miesięczny koszt działania dzierżawy usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="be51d-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="be51d-113">Ten artykuł dotyczy powiązane rozliczeń działalność, która jest oparta na liczbę użytkowników, rozliczeniowy Zaloguj się w podstawie uwierzytelnienia i uwierzytelnienia wieloskładnikowego raportów.</span><span class="sxs-lookup"><span data-stu-id="be51d-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="be51d-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be51d-114">Prerequisites</span></span>
<span data-ttu-id="be51d-115">Przed rozpoczęciem pracy należy wykonać czynności opisane w [wymagania wstępne dotyczące raportowania interfejsów API usługi Azure AD dostęp](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="be51d-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="be51d-116">Tworzenie aplikacji, uzyskać klucz tajny i przyznać jej dostęp prawa do dzierżawy usługi Azure AD B2C raportów.</span><span class="sxs-lookup"><span data-stu-id="be51d-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="be51d-117">*Bash skryptu* i *skrypt w języku Python* zamieszczono przykłady, które również w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="be51d-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="be51d-118">Skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="be51d-118">PowerShell script</span></span>
<span data-ttu-id="be51d-119">Ten skrypt pokazuje tworzenia raportów użycia czterech przy użyciu `TimeStamp` parametru i `ApplicationId` filtru.</span><span class="sxs-lookup"><span data-stu-id="be51d-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="be51d-120">Definicje raportów użycia</span><span class="sxs-lookup"><span data-stu-id="be51d-120">Usage report definitions</span></span>
* <span data-ttu-id="be51d-121">**tenantUserCount**: liczba użytkowników w dzierżawie według typu dostawcy tożsamości, dziennie w ciągu ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="be51d-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="be51d-122">(Opcjonalnie `TimeStamp` filtru zawiera liczby użytkowników z określonej daty do daty bieżącej).</span><span class="sxs-lookup"><span data-stu-id="be51d-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="be51d-123">Raport zawiera:</span><span class="sxs-lookup"><span data-stu-id="be51d-123">The report provides:</span></span>
  * <span data-ttu-id="be51d-124">**TotalUserCount**: liczba wszystkie obiekty użytkowników.</span><span class="sxs-lookup"><span data-stu-id="be51d-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="be51d-125">**OtherUserCount**: liczba użytkowników usługi Azure Active Directory (nie użytkowników usługi Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="be51d-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="be51d-126">**LocalUserCount**: liczba kont użytkowników usługi Azure AD B2C utworzone przy użyciu poświadczeń lokalnych do dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="be51d-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="be51d-127">**AlternateIdUserCount**: liczba użytkowników usługi Azure AD B2C zarejestrowane przy pomocy dostawcy tożsamości zewnętrznych (na przykład, Facebook, konta Microsoft lub innej dzierżawy usługi Azure Active Directory, nazywana także `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="be51d-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="be51d-128">**b2cAuthenticationCountSummary**: Podsumowanie codzienne numer rozliczeniowy uwierzytelnienia w ciągu ostatnich 30 dni dzień, a typ Przepływ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="be51d-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="be51d-129">**b2cAuthenticationCount**: liczbę uwierzytelnień w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="be51d-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="be51d-130">Wartość domyślna to ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="be51d-130">The default is the last 30 days.</span></span>  <span data-ttu-id="be51d-131">(Opcjonalnie: na rozpoczęcie i zakończenie `TimeStamp` parametry definiują w określonym przedziale czasu.) Dane wyjściowe obejmują `StartTimeStamp` (najwcześniejsza data działania dla tej dzierżawy) i `EndTimeStamp` (najnowsza aktualizacja).</span><span class="sxs-lookup"><span data-stu-id="be51d-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="be51d-132">**b2cMfaRequestCountSummary**: podsumowanie liczby codzienne operacje uwierzytelniania wieloskładnikowego, dzień, a typ (SMS lub głosowych).</span><span class="sxs-lookup"><span data-stu-id="be51d-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="be51d-133">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="be51d-133">Limitations</span></span>
<span data-ttu-id="be51d-134">Użytkownik liczba dane są odświeżane co 24 do 48 godzin.</span><span class="sxs-lookup"><span data-stu-id="be51d-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="be51d-135">Uwierzytelnienia są aktualizowane kilka razy dziennie.</span><span class="sxs-lookup"><span data-stu-id="be51d-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="be51d-136">Korzystając z `ApplicationId` filtru odpowiedzi pusty raport może być spowodowane jedną z następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="be51d-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="be51d-137">Identyfikator aplikacji nie istnieje w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="be51d-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="be51d-138">Upewnij się, że jest poprawny.</span><span class="sxs-lookup"><span data-stu-id="be51d-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="be51d-139">Identyfikator aplikacji istnieje, ale nie znaleziono danych w tym okresie raportowania.</span><span class="sxs-lookup"><span data-stu-id="be51d-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="be51d-140">Przejrzyj parametry daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="be51d-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="be51d-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be51d-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="be51d-142">Rachunek miesięczny szacuje dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="be51d-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="be51d-143">W połączeniu z [najbardziej bieżące usługi Azure AD B2C ceny dostępne](https://azure.microsoft.com/pricing/details/active-directory-b2c/), można oszacować dzienne, tygodniowe i miesięczne wykorzystania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="be51d-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="be51d-144">Szacowana jest szczególnie przydatne podczas planowania zmiany w zachowaniu dzierżawy, który może mieć wpływ na całkowity koszt.</span><span class="sxs-lookup"><span data-stu-id="be51d-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="be51d-145">Możesz przejrzeć koszty rzeczywiste w Twojej [połączonej subskrypcji Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="be51d-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="be51d-146">Opcje dla innych formatów wyjściowych</span><span class="sxs-lookup"><span data-stu-id="be51d-146">Options for other output formats</span></span>
<span data-ttu-id="be51d-147">Poniższy kod przedstawia przykłady wysyłanie danych wyjściowych do formatu JSON, listy wartości nazw i XML:</span><span class="sxs-lookup"><span data-stu-id="be51d-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
