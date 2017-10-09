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
ms.openlocfilehash: 4762fffef040f9b409355f9ee0e8cc593e3eea0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-ad-functionality-for-self-service-password-reset"></a>Dostosowywanie funkcji usługi Azure AD dla samoobsługowego resetowania hasła

Profesjonalistów IT toodeploy Samoobsługowe Resetowanie hasła można dostosować hello toomatch doświadczenia użytkowników.

## <a name="customize-hello-contact-your-administrator-link"></a>Dostosowywanie kontaktu hello link do administratora

Nawet jeśli SSPR nie jest włączone, użytkownicy portal resetowania nadal "Skontaktuj się z administratorem" łącze na powitania hasła.  Kliknięcie tego łącza wiadomości e-mail z prośbą o pomoc w odniesieniu do zmiany hasła użytkownika hello administratorami. Ta wiadomość e-mail jest wysyłana toohello następujących adresatów w następującej kolejności hello:

1. Jeśli hello **hasło administratora** rola jest przypisywana, administratorów z tej roli są powiadomienia.
2. Jeśli hasło administratorów nie ma przypisanych, następnie administratorom hello **użytkownika administratora** są powiadamiani o roli
3. Jeśli żaden z poprzednich ról hello zostały przypisane, następnie **Administratorzy globalni** są powiadamiani o

We wszystkich przypadkach są powiadamiani o maksymalnie 100 adresatów.

toofind więcej informacji na temat hello inny administrator ról i sposób ich Zobacz tooassign hello dokumentu [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md)

### <a name="disable-contact-your-administrator-emails"></a>Wyłącz skontaktuj się z administratorem wiadomości e-mail

Jeśli Twoja organizacja nie chce żądań resetowania Administratorzy otrzymywać powiadomienia o hasło, hello następującej konfiguracji można włączyć

* Włącz samoobsługowego resetowania haseł dla wszystkich użytkowników końcowych. Ta opcja jest w obszarze **resetowania hasła > właściwości**.
    * Jeśli nie chcesz, aby użytkownicy tooreset swoje hasła, można określić zakres dostępu tooan pustej grupy **nie zaleca się opcja**.
* Dostosowywanie tooprovide łącza pomocy technicznej hello adres URL sieci web lub mailto: adres, w których użytkownicy mogą używać tooget pomocy. Ta opcja jest w obszarze **resetowania hasła > dostosowania > niestandardowe pomoc techniczna e-mail lub adres URL**.

## <a name="customize-adfs-sign-in-page-for-sspr"></a>Dostosowywanie strony logowania usług AD FS dla usługi SSPR

Administratorzy usług AD FS można dodać łącza tootheir strony logowania przy użyciu wskazówek hello znaleźć w artykule hello [dodawanie opisu strony logowania](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-sign-in-page-description).

Za pomocą polecenia hello, znajdujący się na serwerze usług AD FS dodaje strony logowania usług AD FS toohello łącze umożliwiające przepływu pracy resetowania hasła samoobsługi użytkowników tooenter hello bezpośrednio.

``` Set-ADFSGlobalWebContent -SigninPageDescriptionText "<p><A href=’https://passwordreset.microsoftonline.com’>Can’t access your account?</A></p>" ```

## <a name="customize-hello-sign-in-and-access-panel-look-and-feel"></a>Dostosowywanie hello logowania i dostępu do panelu Wygląd i działanie

Gdy użytkownicy uzyskują dostęp do strony logowania hello, można dostosować logo hello, które pojawia się wraz z toofit obraz strony logowania hello znakowaniu firmy.

Elementy te są przedstawione w hello w następujących okolicznościach:

* Po użytkownik wpisuje swoją nazwę użytkownika
* Użytkownik uzyskuje dostęp do adresu url dostosowane
    * Przez przekazanie hello hasła toohello parametru "godz. pracy" Resetuj strony, takich jak "https://login.microsoftonline.com/?whr=contoso.com"
    * Przez przekazanie hello "nazwa_użytkownika" parametr toohello resetowania hasła strony, takie jak "https://login.microsoftonline.com/?username=admin@contoso.com"

### <a name="graphics-details"></a>Szczegóły grafiki

Hello następujące ustawienia pozwalają toochange hello wizualne cechy hello strony logowania i znajduje się w obszarze **usługi Azure Active Directory**, **firmy znakowania**, **Edytuj firmy znakowania.**

* Obraz strony logowania powinien być PNG lub JPG pliku 1420 x 1200 pikseli i nie większa niż 500KB. Zaleca się jej toobe około 200 KB w celu uzyskania najlepszych wyników.
* Kolor tła strony logowania jest używany podczas połaczeń dużymi opóźnieniami i musi być w formacie szesnastkowym RGB hello.
* Transparent obraz powinien być pikseli 60 x 280 plik PNG lub JPG i nie większa niż 10 KB.
* Kwadratowe logo (normalne i ciemnego motywu) PNG lub JPG 240 x 240 (rozmiar) nie większą niż 10 KB.

### <a name="sign-in-text-options"></a>Opcje logowania tekstu

Witaj następujące ustawienia pozwalają tooadd tekst toohello stronę logowania w odpowiednich tooyour organizacji. Te ustawienia można znaleźć w **usługi Azure Active Directory**, **firmy znakowania**, **znakowanie firmowe do edycji**

* **Wskazówka nazwy użytkownika** zastępuje hello przykładowy tekst someone@example.com na coś bardziej odpowiednie dla użytkowników, zalecane toobe domyślny po lewej stronie, gdy obsługa użytkowników wewnętrznych i zewnętrznych
* **Tekst strony logowania** maksymalnie 256 znaków. Ten tekst jest wyświetlany dowolnym logowanie użytkowników online, a w hello Azure AD Join doświadczenie w systemie Windows 10. Użyj tego tekstu warunków użytkowania, instrukcje i wskazówki dla użytkowników. **Każda osoba, która jest zobacz stronę logowania, więc nie zawierają żadnych poufnych informacji.**

### <a name="keep-me-signed-in-disabled"></a>Nie wylogowuj mnie — wyłączono

Opcja Hello "wylogowuj mnie wyłączone" umożliwia tooremain użytkowników rejestracji podczas Zamknij i otwórz ponownie ich okna przeglądarki. Ta opcja nie będzie mieć wpływu okresy istnienia sesji. To ustawienie znajduje się w obszarze **usługi Azure Active Directory > firmy znakowania > Edytuj firmowe**.

Niektóre funkcje pakietu Office 2010 i SharePoint Online zależy od użytkownicy będą mogli toocheck tego pola. Ukrycie tę opcję, użytkownicy mogą pobrać dodatkowe i nieoczekiwane logowania monitów.

### <a name="directory-name"></a>Nazwa katalogu

Możesz zmienić hello atrybutu nazwy w obszarze **usługi Azure Active Directory > właściwości** tooshow organizacji przyjazną nazwę w portalu hello i automatyzować komunikacji. Ta opcja jest najbardziej widoczne w formie hello zautomatyzowane wiadomości e-mail w formularzach hello, które należy wykonać

* Przyjazna nazwa w wiadomości e-mail "Microsoft w imieniu pokaz firmy CONTOSO"
* Wiersz tematu wiadomości e-mail "CONTOSO demonstracyjna konta e-mail kod weryfikacyjny"

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

