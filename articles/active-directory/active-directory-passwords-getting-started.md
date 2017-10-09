---
title: "Szybki start: Samoobsługowe resetowanie haseł w usłudze Azure AD | Microsoft Docs"
description: "Szybkie wdrażanie samoobsługowego resetowania haseł w usłudze Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Szybki start: Samoobsługowe resetowanie haseł w usłudze Azure AD

> [!IMPORTANT]
> **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Szybkie wdrażanie samoobsługowego resetowania haseł

Samoobsługowego resetowania hasła (SSPR) oferuje prosty oznacza, że dla tooreset użytkowników tooempower Administratorzy IT lub odblokować ich haseł i kont. Witaj system zawiera szczegółowe tootrack raportowania Jeśli użytkownicy korzystają z systemu hello wraz z tooalert powiadomienia możesz toomisuse lub nadużycia.

W tym przewodniku założono, że masz już działającą dzierżawę usługi Azure AD, w wersji próbnej lub licencjonowanej. Jeśli potrzebujesz pomocy, konfigurowanie usługi Azure AD, zobacz artykuł hello [wprowadzenie do korzystania z usługi Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).

1. W istniejącej dzierżawie usługi Azure AD wybierz pozycję **„Resetowanie hasła”**

2. Z hello **"Właściwości"** ekranu, w obszarze opcji hello "Self usługa hasła zresetować włączona" Wybierz jedną z następujących hello
    * Nikt nie — co nie jest możliwe toouse funkcji SSPR
    * Możesz wybrać grupy tylko członkowie określonych usługi Azure AD grupa — są w stanie toouse funkcji SSPR
    * Każdy — wszyscy użytkownicy z kontami w dzierżawie usługi Azure AD są w stanie toouse funkcji SSPR

3. Z hello **"Metod uwierzytelniania"** wybierz ekranu
    * Wiele metod wymagana tooreset — obsługujemy co najmniej jeden lub dwa maksymalnie
    * Toousers dostępne metody - potrzebujemy co najmniej jeden, ale powinna toohave dostępny choice dodatkowe
        * **Wiadomości e-mail** wysyła wiadomość e-mail z kodu użytkownika toohello skonfigurowana adres e-mail uwierzytelniania
        * **Telefon komórkowy** zapewnia hello użytkownika hello wybór tooreceive wywołania lub tekst z tootheir kodu skonfigurowany numer telefon komórkowy
        * **Telefon biurowy** wywołania hello użytkownika z tootheir kodu skonfigurowany numer telefonu biurowego
        * **Pytania zabezpieczające** wymaga toochoose
            * Liczba pytań wymaganych tooregister — Witaj minimum dla pomyślnej rejestracji, co oznacza użytkownika można wybrać tooanswer więcej toocreate puli pytania toopull z. Ta opcja może być ustawiona z 3 – 5 i musi być większa niż lub równa toohello liczba pytań wymaganych tooreset.
                * Niestandardowe pytania można dodać, klikając przycisk "Custom" hello, wybierając pytania zabezpieczające
            * Liczba pytań wymaganych tooreset — można ustawić z 3 – 5 pytania toobe udzielić poprawnej odpowiedzi przed zezwoleniem na toobe hasła użytkownikom Resetowanie lub odblokować.

4. ZALECANE: **"Dostosowania"** pozwala toochange hello "Skontaktuj się z administratorem" łącze toopoint tooa strony lub adresu e-mail należy zdefiniować

5. OPCJONALNIE: hello **"Rejestracji"** ekranu zapewnia administratorom hello opcje:
    * Wymagaj tooregister użytkowników podczas logowania
    * Liczba dni, zanim użytkownicy będą zadawane tooreconfirm ich informacje dotyczące uwierzytelniania

6. OPCJONALNIE: hello **"Powiadomienia"** ekranu zapewnia administratorom hello opcje:
    * Czy powiadamiać użytkowników o resetowaniu hasła?
    * Czy powiadamiać wszystkich administratorów, gdy inni administratorzy zresetują swoje hasło?

**W tym momencie skonfigurowano samoobsługowe resetowanie haseł dla dzierżawy usługi Azure AD**. Można zatrzymać w tym miejscu lub nadal na tooconfigure synchronizacji haseł tooan lokalnej domeny usługi AD.

> [!NOTE]
> Przetestuj samoobsługowe resetowanie haseł na koncie użytkownika. Nie rób tego na koncie administratora, ponieważ firma Microsoft narzuca silne wymagania w zakresie uwierzytelniania dla kont administratorów platformy Azure. Aby uzyskać więcej informacji dotyczących zasad haseł hello administratora, zobacz nasze [artykułu zasad haseł](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Konfigurowanie synchronizacji tooexisting tożsamości źródła

tooenable lokalnej tooAzure synchronizacji tożsamości usługi AD, należy tooinstall i skonfigurować [Azure AD Connect](./connect/active-directory-aadconnect.md) na serwerze w organizacji. Ta aplikacja obsługuje synchronizowanie użytkowników i grup z istniejącej dzierżawy usługi Azure AD tooyour źródła tożsamości.

* [Uaktualnienie z narzędzia DirSync i Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Rozpoczynanie pracy z programem Azure AD Connect przy użyciu ustawień ekspresowych](./connect/active-directory-aadconnect-get-started-express.md)
* [Konfigurowanie funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md#configuring-password-writeback) tooyour lokalnego katalogu kopii toowrite haseł z usługi Azure AD.

## <a name="disabling-self-service-password-reset"></a>Wyłączanie samoobsługowego resetowania haseł

Wyłączanie samoobsługowego resetowania hasła jest tak proste, jak otwieranie dzierżawy usługi Azure AD i będą zbyt**resetowania hasła > właściwości** > Wybierz **Brak** w obszarze **samoobsługowego resetowania hasła Włączone**

### <a name="learn-more"></a>Dowiedz się więcej
Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak tooconfigure samoobsługowego resetowania hasła dla użytkowników. toohello toocontinue toocomplete portalu Azure, które należy wykonać następujące kroki hello link poniżej toohello portalu.

> [!div class="nextstepaction"]
> [Włącz samoobsługowe resetowanie haseł](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

