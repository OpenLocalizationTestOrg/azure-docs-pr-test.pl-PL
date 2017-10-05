---
title: 'Dostosowywanie: Azure AD SSPR | Dokumentacja firmy Microsoft'
description: "Dostosowywanie opcji dla usługi Azure AD samodzielnego resetowania hasła usługi"
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
ms.openlocfilehash: 8b9c120815473b25140b8717f8fdd539c97ebb04
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Dostosowywanie funkcji usługi Azure AD dla samoobsługowego resetowania hasła

Specjaliści IT, które chcą wdrożyć Samoobsługowe Resetowanie hasła można dostosować środowiska, aby dopasować użytkowników.

## <a name="customize-the-contact-your-administrator-link"></a>Dostosowywanie kontaktu link do administratora

Nawet jeśli nie włączono funkcji SSPR portal resetowania użytkownicy nadal "Skontaktuj się z administratorem" łącze hasło.  Kliknięcie tego łącza wiadomości e-mail z prośbą o pomoc w odniesieniu do zmiany hasła administratorami. Ten adres e-mail jest wysyłane do następujących adresatów w następującej kolejności:

1. Jeśli **hasło administratora** rola jest przypisywana, administratorów z tej roli są powiadomienia.
2. Jeśli hasło administratorów nie ma przypisanych, następnie Administratorzy z **użytkownika administratora** są powiadamiani o roli
3. Jeśli żaden z poprzednich role zostały przypisane, następnie **Administratorzy globalni** są powiadamiani o

We wszystkich przypadkach są powiadamiani o maksymalnie 100 adresatów.

Aby dowiedzieć się więcej o różnych administrator ról i przypisywania im można znaleźć w dokumencie [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Wyłącz skontaktuj się z administratorem wiadomości e-mail

Jeśli Twoja organizacja nie chce żądań resetowania Administratorzy otrzymywać powiadomienia o hasło, można włączyć następującą konfigurację

* Włącz samoobsługowego resetowania haseł dla wszystkich użytkowników końcowych. Ta opcja jest w obszarze **resetowania hasła > właściwości**.
    * Jeśli nie chcesz, aby użytkownikom na resetowanie własnych haseł, można określić zakres dostępu do pustej grupy **nie zaleca się opcja**.
* Dostosowywanie link pomocy technicznej, aby podać adres URL sieci web lub mailto: adres, który użytkownicy mogą używać, aby uzyskać pomoc. Ta opcja jest w obszarze **resetowania hasła > dostosowania > niestandardowe pomoc techniczna e-mail lub adres URL**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Dostosowywanie strony logowania usług AD FS dla usługi SSPR

Administratorzy usług AD FS można dodać łącza do strony przy użyciu wskazówek znaleźć w artykule w ich logowania [dodawanie opisu strony logowania](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Za pomocą polecenia znajdujący się na serwerze usług AD FS dodaje łącze do strony logowania usług AD FS, dzięki czemu użytkownicy mogą wprowadzić hasło samoobsługi resetowania bezpośrednio przepływu pracy.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-the-sign-in-and-access-panel-look-and-feel"></a>Dostosowywanie logowania i dostępu do panelu Wygląd i działanie

Gdy użytkownicy uzyskują dostęp do strony logowania, można dostosować logo, które pojawia się wraz z obrazem strony logowania, aby dopasować znakowaniu firmy.

Elementy te są wyświetlane w następujących okolicznościach:

* Po użytkownik wpisuje swoją nazwę użytkownika
* Użytkownik uzyskuje dostęp do adresu url dostosowane
    * Przez przekazanie "godz. pracy" strony, takich jak "https://login.microsoftonline.com/?whr=contoso.com" resetowania parametr hasło
    * Przez przekazanie "nazwa_użytkownika" Parametr hasło strony resetowania, tak samo, jak "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Szczegóły grafiki

Następujące ustawienia pozwalają na zmiany wizualne cechy strony logowania i znajduje się w obszarze **usługi Azure Active Directory**, **firmy znakowania**, **znakowanie firmowe do edycji**

* Obraz strony logowania powinien być PNG lub JPG pliku 1420 x 1200 pikseli i nie większa niż 500KB. Firma Microsoft zaleca, aby wartość była około 200 KB w celu uzyskania najlepszych wyników.
* Kolor tła strony logowania jest używany podczas połaczeń dużymi opóźnieniami i musi być w formacie szesnastkowym RGB.
* Transparent obraz powinien być pikseli 60 x 280 plik PNG lub JPG i nie większa niż 10 KB.
* Kwadratowe logo (normalne i ciemnego motywu) PNG lub JPG 240 x 240 (rozmiar) nie większą niż 10 KB.

### <a name="sign-in-text-options"></a>Opcje logowania tekstu

Następujące ustawienia pozwalają na dodawanie tekstu do strony logowania istotne dla Twojej organizacji. Te ustawienia można znaleźć w **usługi Azure Active Directory**, **firmy znakowania**, **znakowanie firmowe do edycji**

* **Wskazówka nazwy użytkownika** zastępuje tekst przykład someone@example.com na coś bardziej odpowiednie dla użytkowników, zaleca, aby pozostawić domyślne podczas obsługi użytkowników wewnętrznych i zewnętrznych
* **Tekst strony logowania** maksymalnie 256 znaków. Ten tekst jest wyświetlany wszędzie logowanie użytkowników online i w środowisku Azure AD Join w systemie Windows 10. Użyj tego tekstu warunków użytkowania, instrukcje i wskazówki dla użytkowników. **Każda osoba, która jest zobacz stronę logowania, więc nie zawierają żadnych poufnych informacji.**

### <a name="keep-me-signed-in-disabled"></a>Nie wylogowuj mnie — wyłączono

Opcji "Zachowaj wylogowuj mnie wyłączone" umożliwia użytkownikom wylogować po zamknięciu i ponownie otworzyć ich okna przeglądarki. Ta opcja nie będzie mieć wpływu okresy istnienia sesji. To ustawienie znajduje się w obszarze **usługi Azure Active Directory > firmy znakowania > Edytuj firmowe**.

Niektóre funkcje pakietu Office 2010 i SharePoint Online zależy od użytkownicy będą mogli przeprowadzić zaznacz to pole wyboru. Ukrycie tę opcję, użytkownicy mogą pobrać dodatkowe i nieoczekiwane logowania monitów.

### <a name="directory-name"></a>Nazwa katalogu

Można zmienić atrybutu nazwy w obszarze **usługi Azure Active Directory > właściwości** pokazanie organizacji przyjazną nazwę widoczne w portalu i automatyczne komunikację. Ta opcja jest najbardziej widoczne w formularzu zautomatyzowane wiadomości e-mail w kolejnych formularzach

* Przyjazna nazwa w wiadomości e-mail "Microsoft w imieniu pokaz firmy CONTOSO"
* Wiersz tematu wiadomości e-mail "CONTOSO demonstracyjna konta e-mail kod weryfikacyjny"

## <a name="next-steps"></a>Następne kroki

Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami
* [**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? — Odpowiedzi na wszystkie nurtujące Cię pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł

