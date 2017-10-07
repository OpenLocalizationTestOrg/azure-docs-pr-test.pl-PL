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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Wdrażanie resetowania hasła bez konieczności rejestrowania użytkownika końcowego

Wdrażanie funkcji samoobsługowego resetowania hasła (SSPR) wymaga się toobe danych uwierzytelniania. Niektóre organizacje mają użytkownikom wprowadź dane uwierzytelniania samodzielnie, ale w wielu organizacjach preferowane toosynchronize z istniejącymi danymi w usłudze Active Directory. Prawidłowo sformatowane dane w katalogu lokalnego i skonfigurować [Azure AD Connect przy użyciu ustawień ekspresowych](./connect/active-directory-aadconnect-get-started-express.md), że dane stają się dostępne tooAzure AD i SSPR z bez udziału użytkownika.

Wszystkie numery telefonów musi być w formacie hello + CountryCode PhoneNumber przykład: + 1 4255551234 toowork poprawnie.

> [!NOTE]
> Resetowanie hasła nie obsługuje rozszerzeń telefonu. Nawet w hello 4255551234 + 1 X 12345 format rozszerzenia zostały usunięte przed wykonaniem hello.

## <a name="fields-populated"></a>Pól

Jeśli używasz ustawienia domyślne hello hello Azure AD Connect po mapowania zostały wprowadzone.

| Lokalne usługi AD | Azure AD | Azure AD Authentication informacje kontaktowe |
| --- | --- | --- |
| TelephoneNumber | Telefon biurowy | Alternatywne telefonu |
| Telefon komórkowy | Telefon komórkowy | Numer telefonu |


## <a name="security-questions-and-answers"></a>Pytania zabezpieczające i odpowiedzi

Pytania zabezpieczające i odpowiedzi są bezpiecznie przechowywane w dzierżawie usługi Azure AD i są tylko dostępny toousers za pośrednictwem hello [portal rejestracji SSPR](https://aka.ms/ssprsetup). Administratorzy nie można wyświetlić ani zmodyfikować hello zawartość innym użytkownikom pytania i odpowiedzi.

### <a name="what-happens-when-a-user-registers"></a>Co się dzieje, gdy użytkownik rejestruje

Gdy użytkownik rejestruje, strony rejestracji hello ustawia hello następujące pola:

* Numer telefonu uwierzytelniania
* Uwierzytelnianie wiadomości E-mail
* Pytania zabezpieczające i odpowiedzi

Jeśli podano wartość **telefon komórkowy** lub **alternatywny adres E-mail**, użytkownicy mogą od razu używać tooreset tych wartości haseł, nawet jeśli ich nie został zarejestrowany w usłudze hello. Ponadto użytkownicy zobaczyć te wartości podczas rejestrowania dla powitania po raz pierwszy, a ich modyfikacji, jeśli chcesz, aby ich. Po ich pomyślnie zarejestrować, te wartości zostaną utrwalone w hello **numer telefonu uwierzytelniania** i **E-mail uwierzytelniania** pola odpowiednio.

## <a name="set-and-read-authentication-data-using-powershell"></a>Ustaw i odczytywanie danych uwierzytelniania przy użyciu programu PowerShell

Witaj kolejnych pól można ustawić za pomocą programu PowerShell

* Alternatywny adres E-mail
* Telefon komórkowy
* Telefon biurowy — można ustawiać tylko, jeśli nie synchronizacji z katalogiem lokalnym

### <a name="using-powershell-v1"></a>Przy użyciu programu PowerShell w wersji 1

tooget uruchomiona, należy za[Pobierz i zainstaluj moduł programu PowerShell usługi Azure AD hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Gdy jest zainstalowany, można wykonać czynności hello, które wykonują tooconfigure każdego pola.

#### <a name="set-authentication-data-with-powershell-v1"></a>Zestaw danych uwierzytelniania za pomocą programu PowerShell w wersji 1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Odczyt danych uwierzytelniania z PowerShellPowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Numer telefonu uwierzytelniania i uwierzytelniania wiadomości E-mail mogą być odczytywane tylko przy użyciu programu Powershell w wersji 1 przy użyciu hello polecenia poniżej

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Przy użyciu programu PowerShell w wersji 2

tooget uruchomiona, należy za[Pobierz i zainstaluj moduł programu PowerShell hello Azure AD w wersji 2](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Gdy jest zainstalowany, można wykonać czynności hello, które wykonują tooconfigure każdego pola.

tooinstall szybko z ostatnie wersjami programu PowerShell, które obsługują moduł instalacji, uruchom następujące polecenia (pierwszy wiersz hello sprawdza toosee Jeśli jest już zainstalowana):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Zestaw danych uwierzytelniania za pomocą programu PowerShell w wersji 2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Odczyt danych uwierzytelniania za pomocą programu PowerShell w wersji 2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR
