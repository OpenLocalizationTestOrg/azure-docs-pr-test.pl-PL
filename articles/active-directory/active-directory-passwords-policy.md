---
title: 'Zasady: Azure AD SSPR | Dokumentacja firmy Microsoft'
description: "Azure AD samoobsługowego resetowania hasła opcji zasad"
services: active-directory
keywords: "Zarządzanie hasłami w usłudze Active directory, zarządzanie hasłami, usługi Azure AD samodzielnego resetowania hasła usługi"
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
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Ograniczenia w usłudze Azure Active Directory i zasad haseł

W tym artykule opisano zasady haseł hello i wymagania dotyczące złożoności skojarzone z kont użytkowników przechowywanych w dzierżawie usługi Azure AD.

## <a name="administrator-password-policy-differences"></a>Różnice zasad hasła administratora

Firma Microsoft wymusza silne domyślne zasady **dwóch bram** w przypadku resetowania hasła dla dowolnej roli administratora platformy Azure (np. Administrator globalny, Administrator pomocy technicznej, Administrator haseł itp.)

To powoduje wyłączenie administratorów za pomocą pytań zabezpieczających i wymusza hello poniżej.

Dwa gate zasady wymagające dwóch rodzajów danych uwierzytelniania (adres e-mail **i** numer telefonu), stosuje się w następujących okoliczności hello

* Wszystkie role administratora platformy Azure
  * Administrator pomocy technicznej
  * Administrator pomocy technicznej usługi
  * Administrator rozliczeń
  * Obsługa Tier1 partnera
  * Obsługa Tier2 partnera
  * Administrator usługi Exchange
  * Administrator usługi Lync
  * Administrator konta użytkownika
  * Składniki zapisywania katalogu
  * Administrator globalny Administrator/firmy
  * Administrator usługi programu SharePoint
  * Administrator zgodności
  * Administrator aplikacji
  * Administrator zabezpieczeń
  * Administrator ról uprzywilejowanych
  * Administrator usługi Intune
  * Administrator usługi serwera Proxy aplikacji
  * Administrator programu CRM usługi
  * Administrator usługi Power BI
  
* upływie 30 dni w ramach próbnego **lub**
* Występuje niestandardowych domeny (contoso.com) **lub**
* Azure AD Connect synchronizuje tożsamości z katalogu lokalnego

### <a name="exceptions"></a>Wyjątki
Zasady co brama, wymagających jednego elementu danych uwierzytelniania (adres e-mail **lub** numer telefonu), stosuje się w następujących okoliczności hello

* Pierwsze 30 dni korzystania z wersji próbnej **lub**
* Nie ma domen niestandardowych (*. onmicrosoft.com) **i** Azure AD Connect nie synchronizuje tożsamości


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>UserPrincipalName zasady dotyczące kont użytkowników tooall

Każdego konta użytkownika, który wymaga toosign w tooAzure AD musi mieć wartość atrybutu unikatowego użytkownika głównej nazwy (UPN) skojarzonych z jego konta. Hello tabelę poniżej przedstawiono, który hello zasady stosowane tooboth lokalnego konta użytkownika usługi Active Directory zsynchronizowanych kont użytkownika tylko do toocloud i toohello chmury.

| Właściwość | Wymagania dotyczące UserPrincipalName |
| --- | --- |
| Znaki są dozwolone |<ul> <li>A-Z</li> <li>- z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Znaki nie są dozwolone |<ul> <li>Wszelkie "@" znak, który nie jest oddzielenie hello nazwy użytkownika z hello domeny.</li> <li>Nie może zawierać znaku kropki "." hello bezpośrednio poprzednie "@" — symbol</li></ul> |
| Ograniczenia długości |<ul> <li>Łączna długość nie może przekraczać 113 znaków</li><li>64 znaki, przed hello "@" — symbol</li><li>48 znaków po hello "@" — symbol</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Zasady haseł, które są stosowane tylko konta użytkowników toocloud

Witaj w poniższej tabeli opisano ustawienia zasad haseł dostępne hello, które mogą być zastosowane toouser konta, które są tworzone i zarządzane w usłudze Azure AD.

| Właściwość | Wymagania |
| --- | --- |
| Znaki są dozwolone |<ul><li>A-Z</li><li>- z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Znaki nie są dozwolone |<ul><li>Znaki Unicode</li><li>Spacje</li><li> **Silne hasła tylko**: nie może zawierać znaku kropki "." hello bezpośrednio poprzednie "@" — symbol</li></ul> |
| Ograniczenia haseł |<ul><li>minimalnej 8 znaków i maksymalnie 16 znaków.</li><li>**Silne hasła tylko**: wymaga 3 z 4 hello poniżej:<ul><li>Małe litery</li><li>Wielkie litery</li><li>Cyfry (0 – 9)</li><li>Symbole (zobacz powyżej ograniczeń hasła)</li></ul></li></ul> |
| Okres wygasania haseł |<ul><li>Wartość domyślna: **90** dni </li><li>Wartość jest można skonfigurować za pomocą polecenia cmdlet Set-MsolPasswordPolicy hello hello Azure Active Directory modułu dla środowiska Windows PowerShell.</li></ul> |
| Powiadomienie o wygaśnięciu hasła |<ul><li>Wartość domyślna: **14** dni (do wygaśnięcia hasła)</li><li>Można skonfigurować za pomocą polecenia cmdlet Set-MsolPasswordPolicy hello jest wartość.</li></ul> |
| Wygaśnięcia hasła |<ul><li>Wartość domyślna: **false** dni (wskazuje, że wygaśnięcie hasła jest włączona) </li><li>Wartość można skonfigurować dla poszczególnych kont użytkowników przy użyciu polecenia cmdlet Set-MsolUser hello. </li></ul> |
| Hasło **zmienić** historii |Hasło ostatnio **nie** można użyć ponownie po **zmiana** hasła. |
| Hasło **zresetować** historii | Hasło ostatnio **może** można użyć ponownie po **Resetowanie** zapomniane hasło. |
| Blokada konta |Po 10 nieudanych próbach zalogowania (nieprawidłowe hasło) hello użytkownika zostanie zablokowane w ciągu jednej minuty. Dodatkowo niepoprawne prób zalogowania blokady użytkownika hello na zwiększenie wartości czasu trwania. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Ustawianie zasad wygasania haseł w usłudze Azure Active Directory

Administrator globalny dla usługi w chmurze firmy Microsoft można użyć tooset Microsoft Azure Active Directory modułu dla środowiska Windows PowerShell hello hasła użytkowników nie tooexpire. Umożliwia także hello tooremove poleceń cmdlet nigdy nie wygasa konfiguracji lub toosee hasła użytkownika, które są skonfigurowane nie tooexpire środowiska Windows PowerShell. Niniejsze wytyczne mają zastosowanie tooother dostawców, takich jak Microsoft Intune i Office 365, które również polegać na Microsoft Azure Active Directory dla tożsamości i usługi katalogowe.

> [!NOTE]
> Tylko haseł dla kont użytkowników, które nie są synchronizowane przez synchronizacji katalogów można skonfigurować toonot wygaśnie. Aby uzyskać więcej informacji na temat synchronizacji katalogów zobacz[AD z usługą Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Ustawianie lub Sprawdzanie zasad haseł przy użyciu programu PowerShell

tooget uruchomiona, należy za[Pobierz i zainstaluj moduł programu PowerShell usługi Azure AD hello](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Gdy jest zainstalowany, można wykonać kroki hello poniżej tooconfigure każdego pola.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>Jak toocheck zasady wygasania hasła
1. Połącz tooWindows programu PowerShell przy użyciu poświadczeń administratora firmy.
2. Wykonaj jedną z hello następującego polecenia:

   * toosee Określa, czy hasło jednego użytkownika ustawiono toonever ważność, uruchom następujące polecenia cmdlet, za pomocą hello nazwa główna użytkownika (UPN) hello (na przykład aprilr@contoso.onmicrosoft.com) lub identyfikator użytkownika hello hello użytkownika ma toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee Witaj "Hasło nigdy nie wygasa" ustawienia dla wszystkich użytkowników, uruchom następujące polecenie cmdlet hello:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Ustaw tooexpire hasła

1. Połącz tooWindows programu PowerShell przy użyciu poświadczeń administratora firmy.
2. Wykonaj jedną z hello następującego polecenia:

   * hasło hello tooset jednego użytkownika, aby hello hasło wygaśnie, uruchom następujące polecenia cmdlet, za pomocą hello nazwa główna użytkownika (UPN) hello lub hello identyfikator użytkownika, powitalne użytkownika:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * tooset hello hasła wszystkich użytkowników w organizacji hello tak, aby wygasną, należy użyć hello następującego polecenia cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Zestaw toonever hasło wygaśnie

1. Połącz tooWindows programu PowerShell przy użyciu poświadczeń administratora firmy.
2. Wykonaj jedną z hello następującego polecenia:

   * hasło hello tooset toonever jednego użytkownika wygaśnie, uruchom następujące polecenia cmdlet, za pomocą hello nazwa główna użytkownika (UPN) hello lub hello identyfikator użytkownika, powitalne użytkownika:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * tooset hello hasła wszystkich użytkowników hello w organizacji toonever ważność, uruchom następujące polecenie cmdlet hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR
