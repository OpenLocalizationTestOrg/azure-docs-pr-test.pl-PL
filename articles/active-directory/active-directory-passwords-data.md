---
title: "Wymagania dotyczące danych usługi Azure AD SSPR | Dokumentacja firmy Microsoft"
description: "Resetuj danych wymagania dotyczące usługi Azure AD samoobsługi hasła i w jaki sposób toosatisfy ich"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="3c989-103">Wdrażanie resetowania hasła bez konieczności rejestrowania użytkownika końcowego</span><span class="sxs-lookup"><span data-stu-id="3c989-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="3c989-104">Wdrażanie funkcji samoobsługowego resetowania hasła (SSPR) wymaga się toobe danych uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="3c989-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="3c989-105">Niektóre organizacje mają użytkownikom wprowadź dane uwierzytelniania samodzielnie, ale w wielu organizacjach preferowane toosynchronize z istniejącymi danymi w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c989-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="3c989-106">Prawidłowo sformatowane dane w katalogu lokalnego i skonfigurować [Azure AD Connect przy użyciu ustawień ekspresowych](./connect/active-directory-aadconnect-get-started-express.md), że dane stają się dostępne tooAzure AD i SSPR z bez udziału użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c989-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="3c989-107">Wszystkie numery telefonów musi być w formacie hello + CountryCode PhoneNumber przykład: + 1 4255551234 toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="3c989-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="3c989-108">Resetowanie hasła nie obsługuje rozszerzeń telefonu.</span><span class="sxs-lookup"><span data-stu-id="3c989-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="3c989-109">Nawet w hello 4255551234 + 1 X 12345 format rozszerzenia zostały usunięte przed wykonaniem hello.</span><span class="sxs-lookup"><span data-stu-id="3c989-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="3c989-110">Pól</span><span class="sxs-lookup"><span data-stu-id="3c989-110">Fields populated</span></span>

<span data-ttu-id="3c989-111">Jeśli używasz ustawienia domyślne hello hello Azure AD Connect po mapowania zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="3c989-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="3c989-112">Lokalne usługi AD</span><span class="sxs-lookup"><span data-stu-id="3c989-112">On-premises AD</span></span> | <span data-ttu-id="3c989-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c989-113">Azure AD</span></span> | <span data-ttu-id="3c989-114">Azure AD Authentication informacje kontaktowe</span><span class="sxs-lookup"><span data-stu-id="3c989-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c989-115">TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="3c989-115">telephoneNumber</span></span> | <span data-ttu-id="3c989-116">Telefon biurowy</span><span class="sxs-lookup"><span data-stu-id="3c989-116">Office phone</span></span> | <span data-ttu-id="3c989-117">Alternatywne telefonu</span><span class="sxs-lookup"><span data-stu-id="3c989-117">Alternate phone</span></span> |
| <span data-ttu-id="3c989-118">Telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="3c989-118">mobile</span></span> | <span data-ttu-id="3c989-119">Telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="3c989-119">Mobile phone</span></span> | <span data-ttu-id="3c989-120">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="3c989-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="3c989-121">Pytania zabezpieczające i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3c989-121">Security questions and answers</span></span>

<span data-ttu-id="3c989-122">Pytania zabezpieczające i odpowiedzi są bezpiecznie przechowywane w dzierżawie usługi Azure AD i są tylko dostępny toousers za pośrednictwem hello [portal rejestracji SSPR](https://aka.ms/ssprsetup).</span><span class="sxs-lookup"><span data-stu-id="3c989-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="3c989-123">Administratorzy nie można wyświetlić ani zmodyfikować hello zawartość innym użytkownikom pytania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3c989-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="3c989-124">Co się dzieje, gdy użytkownik rejestruje</span><span class="sxs-lookup"><span data-stu-id="3c989-124">What happens when a user registers</span></span>

<span data-ttu-id="3c989-125">Gdy użytkownik rejestruje, strony rejestracji hello ustawia hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="3c989-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="3c989-126">Numer telefonu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="3c989-126">Authentication Phone</span></span>
* <span data-ttu-id="3c989-127">Uwierzytelnianie wiadomości E-mail</span><span class="sxs-lookup"><span data-stu-id="3c989-127">Authentication Email</span></span>
* <span data-ttu-id="3c989-128">Pytania zabezpieczające i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3c989-128">Security Questions and Answers</span></span>

<span data-ttu-id="3c989-129">Jeśli podano wartość **telefon komórkowy** lub **alternatywny adres E-mail**, użytkownicy mogą od razu używać tooreset tych wartości haseł, nawet jeśli ich nie został zarejestrowany w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="3c989-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="3c989-130">Ponadto użytkownicy zobaczyć te wartości podczas rejestrowania dla powitania po raz pierwszy, a ich modyfikacji, jeśli chcesz, aby ich.</span><span class="sxs-lookup"><span data-stu-id="3c989-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="3c989-131">Po ich pomyślnie zarejestrować, te wartości zostaną utrwalone w hello **numer telefonu uwierzytelniania** i **E-mail uwierzytelniania** pola odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3c989-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="3c989-132">Ustaw i odczytywanie danych uwierzytelniania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c989-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="3c989-133">Witaj kolejnych pól można ustawić za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c989-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="3c989-134">Alternatywny adres E-mail</span><span class="sxs-lookup"><span data-stu-id="3c989-134">Alternate Email</span></span>
* <span data-ttu-id="3c989-135">Telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="3c989-135">Mobile Phone</span></span>
* <span data-ttu-id="3c989-136">Telefon biurowy — można ustawiać tylko, jeśli nie synchronizacji z katalogiem lokalnym</span><span class="sxs-lookup"><span data-stu-id="3c989-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="3c989-137">Przy użyciu programu PowerShell w wersji 1</span><span class="sxs-lookup"><span data-stu-id="3c989-137">Using PowerShell V1</span></span>

<span data-ttu-id="3c989-138">tooget uruchomiona, należy za[Pobierz i zainstaluj moduł programu PowerShell usługi Azure AD hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span><span class="sxs-lookup"><span data-stu-id="3c989-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="3c989-139">Gdy jest zainstalowany, można wykonać czynności hello, które wykonują tooconfigure każdego pola.</span><span class="sxs-lookup"><span data-stu-id="3c989-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="3c989-140">Zestaw danych uwierzytelniania za pomocą programu PowerShell w wersji 1</span><span class="sxs-lookup"><span data-stu-id="3c989-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="3c989-141">Odczyt danych uwierzytelniania z PowerShellPowerShell V1</span><span class="sxs-lookup"><span data-stu-id="3c989-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="3c989-142">Numer telefonu uwierzytelniania i uwierzytelniania wiadomości E-mail mogą być odczytywane tylko przy użyciu programu Powershell w wersji 1 przy użyciu hello polecenia poniżej</span><span class="sxs-lookup"><span data-stu-id="3c989-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="3c989-143">Przy użyciu programu PowerShell w wersji 2</span><span class="sxs-lookup"><span data-stu-id="3c989-143">Using PowerShell V2</span></span>

<span data-ttu-id="3c989-144">tooget uruchomiona, należy za[Pobierz i zainstaluj moduł programu PowerShell hello Azure AD w wersji 2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="3c989-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="3c989-145">Gdy jest zainstalowany, można wykonać czynności hello, które wykonują tooconfigure każdego pola.</span><span class="sxs-lookup"><span data-stu-id="3c989-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="3c989-146">tooinstall szybko z ostatnie wersjami programu PowerShell, które obsługują moduł instalacji, uruchom następujące polecenia (pierwszy wiersz hello sprawdza toosee Jeśli jest już zainstalowana):</span><span class="sxs-lookup"><span data-stu-id="3c989-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="3c989-147">Zestaw danych uwierzytelniania za pomocą programu PowerShell w wersji 2</span><span class="sxs-lookup"><span data-stu-id="3c989-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="3c989-148">Odczyt danych uwierzytelniania za pomocą programu PowerShell w wersji 2</span><span class="sxs-lookup"><span data-stu-id="3c989-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="3c989-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c989-149">Next steps</span></span>

<span data-ttu-id="3c989-150">Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c989-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="3c989-151">[**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c989-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="3c989-152">[**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c989-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="3c989-153">[**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj</span><span class="sxs-lookup"><span data-stu-id="3c989-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="3c989-154">[**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.</span><span class="sxs-lookup"><span data-stu-id="3c989-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="3c989-155">[**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie</span><span class="sxs-lookup"><span data-stu-id="3c989-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="3c989-156">[**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="3c989-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="3c989-157">[**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa</span><span class="sxs-lookup"><span data-stu-id="3c989-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="3c989-158">[**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak?</span><span class="sxs-lookup"><span data-stu-id="3c989-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="3c989-159">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="3c989-159">Why?</span></span> <span data-ttu-id="3c989-160">Co?</span><span class="sxs-lookup"><span data-stu-id="3c989-160">What?</span></span> <span data-ttu-id="3c989-161">Gdzie?</span><span class="sxs-lookup"><span data-stu-id="3c989-161">Where?</span></span> <span data-ttu-id="3c989-162">Kto?</span><span class="sxs-lookup"><span data-stu-id="3c989-162">Who?</span></span> <span data-ttu-id="3c989-163">Kiedy?</span><span class="sxs-lookup"><span data-stu-id="3c989-163">When?</span></span> <span data-ttu-id="3c989-164">-Tooquestions tooask chciał zawsze odpowiada</span><span class="sxs-lookup"><span data-stu-id="3c989-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="3c989-165">[**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR</span><span class="sxs-lookup"><span data-stu-id="3c989-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
