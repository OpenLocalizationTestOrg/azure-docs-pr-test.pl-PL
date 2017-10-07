---
title: "Wdrażanie: Samoobsługowe resetowanie haseł w usłudze Azure AD | Microsoft Docs"
description: "Porady pomagające w pomyślnym wdrażaniu samoobsługowego resetowania haseł w usłudze Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>Wdrażanie resetowania haseł dla użytkowników

Większość klientów kroków hello kolejnych tooensure smooth wdrażanie funkcji SSPR.

1. [Włączanie resetowania haseł w katalogu](active-directory-passwords-getting-started.md)
2. [Konfigurowanie lokalnych uprawnień usługi AD do zapisywania zwrotnego haseł](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [Konfigurowanie funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md#configuring-password-writeback) tooyour lokalnego katalogu kopii toowrite haseł z usługi Azure AD
4. [Przypisywanie i weryfikowanie wymaganych licencji](active-directory-passwords-licensing.md)
5. Jeśli chcesz, aby tooroll się stopniowo, możesz można opcjonalnie limit resetowania hasła tooa grupy użytkowników tooroll się funkcja hello powoli wraz z upływem czasu. toodo ustawić hello **samoobsługowego hasła zresetować włączona usługa** Przełącz z **każdy** za**grupy** i wybierz tooenable grupy zabezpieczeń, do resetowania hasła. Witaj Członkowie tej grupy muszą mieć przypisane licencje toothem i jest tooenable doskonały sposób [grupy na podstawie licencjonowania](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing).
6. Wypełnij hello minimalny zestaw [dane uwierzytelniania](active-directory-passwords-data.md)zgodnie z zasadami.
7. Pokazuje sposób użytkownicy toouse SSPR, wysyłając je tooshow instrukcje je jak tooregister i w jaki sposób tooreset.
    > [!NOTE]
    > Przetestuj samoobsługowe resetowanie haseł na koncie użytkownika. Nie rób tego na koncie administratora, ponieważ firma Microsoft narzuca silne wymagania w zakresie uwierzytelniania dla kont administratorów platformy Azure. Aby uzyskać więcej informacji dotyczących zasad haseł hello administratora, zobacz nasze [artykułu nowości](active-directory-passwords-how-it-works.md).

8. Można wybrać tooenforce rejestracji w dowolnym momencie, a wymagają tooreconfirm użytkownikom ich informacji o uwierzytelnianiu, po upływie pewnego czasu. Jeśli nie chcesz, aby Twoje tooregister toohave użytkowników, możesz [wdrażanie resetowania hasła bez konieczności rejestracji użytkowników końcowych](active-directory-passwords-data.md).
9. Wraz z upływem czasu, przejrzyj użytkownikom rejestrowanie i przy użyciu wyświetlając hello [raportowania dostarczane przez usługę Azure AD](active-directory-passwords-reporting.md).

## <a name="email-based-rollout"></a>Wdrożenie bazujące na poczcie e-mail

Wielu klientów Znajdź kampania wiadomości e-mail z instrukcjami proste toouse jest hello Najprostszym sposobem tooget użytkowników toouse SSPR. [Utworzono trzy proste wiadomości e-mail, których można użyć jako toohelp szablonów w wdrożenia.](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **Wkrótce** wiadomości e-mail używany w tygodniach hello lub dni, po którym użytkownicy toolet wdrażania wiedzieli, muszą toodo coś toobe szablonu.
* **Teraz dostępne** e-mail dzień hello toobe używany szablon tooregister użytkowników toodrive uruchamiania i Potwierdź ich dane uwierzytelniania, aby mogli oni korzystać SSPR, gdy są one wymagane.
* **Zarejestruj się monitu** szablonów dla kilku dni tooweeks wiadomości e-mail po tooregister użytkowników tooremind wdrożenia i Potwierdź ich danych uwierzytelniania.

## <a name="creating-your-own-password-portal"></a>Tworzenie własnego portalu haseł

Większości klientów większych wybierz toohost strony sieci Web i utworzyć wpis DNS, takich jak https://passwords.contoso.com katalog główny. One wypełniania tej strony do resetowania hasła usługi Azure AD toohello łącza, resetowania hasła rejestracji, zmiana haseł do portali i innych informacji specyficznych dla organizacji. W wiadomości e-mail lub ulotki, zostaną wysłane, można następnie dołączyć marką, łatwych do zapamiętania, że użytkownicy, można przejść toowhen potrzebują usługi hello toouse adres URL.

* Portal resetowania haseł — https://passwordreset.microsoftonline.com/
* Portal rejestracji w funkcji resetowania haseł — http://aka.ms/ssprsetup
* Portal zmiany haseł — https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>Korzystanie z rejestracji wymuszonej

Jeśli chcesz tooregister Twojego użytkowników do resetowania hasła, możesz wymusić ich tooregister po zalogowaniu przy użyciu usługi Azure AD. Tę opcję można włączyć w Twoim katalogu **resetowania hasła** bloku przez włączenie hello **tooRegister wymagają użytkowników podczas logowania** opcji na powitania **rejestracji** Karta.

Administratorzy mogą wymagać od użytkowników toore — rejestracja po upływie określonego czasu przez ustawienie hello **liczbę dni, zanim użytkownicy będą zadawane tooreconfirm ich informacje dotyczące uwierzytelniania** między 0 730 dni.

Po włączeniu tej opcji użytkownicy logujący zostanie wyświetlony komunikat z informacją o administratora wymagane, ich tooverify ich informacje dotyczące uwierzytelniania.

## <a name="populate-authentication-data"></a>Wypełnianie danych uwierzytelniania

Jeśli zostanie [wypełnić dane uwierzytelniania dla użytkowników](active-directory-passwords-data.md), następnie użytkownicy nie muszą tooregister dla resetowania przed stanie toouse SSPR hasła. Tak długo, jak użytkownicy mają hello danych uwierzytelniania zdefiniowane, które spełniają zasady resetowania hasła hello zdefiniowane, użytkownicy będą mogli tooreset haseł.

## <a name="disabling-self-service-password-reset"></a>Wyłączanie samoobsługowego resetowania haseł

Wyłączanie samoobsługowego resetowania hasła jest tak proste, jak otwieranie dzierżawy usługi Azure AD i będą zbyt**resetowania hasła**, **właściwości**i wybierając polecenie **nikt nie** w obszarze  **Samodzielne resetowanie haseł włączone**

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR
