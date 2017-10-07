---
title: "Często zadawane pytania: Azure AD SSPR | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure AD samoobsługi hasła resetowania"
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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Często zadawane pytania dotyczące zarządzania hasłami

powitania po są niektóre często zadawane pytania wszystkich czynności związanych z toopassword resetowania.

Jeśli masz pytania ogólne dotyczące usługi Azure AD i hasło samodzielnego resetowania, który nie ma odpowiedzi w tym miejscu, można zadawać społeczności hello pomocy na powitania [fora usługi Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Członkowie społeczności hello obejmują Engineers, menedżerów produktu MVP i twarzy specjalistów IT.

Często zadawane pytania jest podzielony na powitania następujące sekcje:

* [**Pytania dotyczące rejestracji resetowania hasła**](#password-reset-registration)
* [**Pytania dotyczące resetowania hasła**](#password-reset)
* [**Pytania dotyczące zmiany hasła**](#password-change)
* [**Raporty pytania dotyczące zarządzania hasłami**](#password-management-reports)
* [**Pytania dotyczące funkcji zapisywania zwrotnego haseł**](#password-writeback)

## <a name="password-reset-registration"></a>Rejestracja resetowania haseł
* **Pytanie: czy Moi użytkownicy rejestrowanie własnych danych resetowania hasła?**

  > **Odpowiedź:** tak, jak długo resetowania hasła jest włączona i są one licencjonowane, mogą one portalu rejestracji resetowania haseł toohello pod adresem http://aka.ms/ssprsetup tooregister ich informacje dotyczące uwierzytelniania. Użytkownicy mogą również zarejestrować przez przechodzi do panelu dostępu toohello pod adresem http://myapps.microsoft.com, klikając kartę profil hello, a polecenie hello rejestru dla opcji resetowania hasła.
  >
  >
* **Q: czy można zdefiniować dane resetowania hasła w imieniu użytkowników?**

  > **Odpowiedź:** tak, możesz to zrobić z hello Azure AD Connect, programu PowerShell, [portalu Azure](https://portal.azure.com), lub portalu administracyjnego Office hello. Aby uzyskać więcej informacji, zobacz artykuł hello [dane używane przez usługi Azure AD samoobsługowego resetowania hasła](active-directory-passwords-data.md).
  >
  >
* **Pytanie: czy można synchronizować dane odpowiedzi na pytania zabezpieczające z lokalnie?**

  > **Odpowiedź:** nie jest to możliwe dzisiaj.
  >
  >
* **Pytanie: czy Moi użytkownicy zarejestrować danych w taki sposób, że inni użytkownicy nie widzą te dane?**

  > **Odpowiedź:** tak, gdy użytkownicy zarejestrować danych do pól prywatnych uwierzytelniania, które są widoczne przez użytkownika administratorzy globalni i hello tylko przy użyciu hello portalu resetowania haseł rejestracji jest zapisywany.
    >
    > [!NOTE]
    > Jeśli **konto administratora platformy Azure** rejestruje numer telefonu uwierzytelniania również są umieszczane w pole telefonu komórkowego hello i jest widoczny.
    >
  >
  >
* **Pytanie: czy Moi użytkownicy mają toobe zarejestrowane przed użyciem resetowania hasła?**

  > **Odpowiedź:** nie, jeśli zdefiniujesz wystarczających informacji uwierzytelniania w ich imieniu użytkownicy nie mają tooregister. Działania resetowania hasła, tak długo, jak długo mają poprawnie sformatowana danych przechowywanych w hello odpowiednich pól w katalogu hello.
  >
  >
* **Pytanie: można zsynchronizować lub ustawiają pola numer telefonu uwierzytelniania, uwierzytelniania wiadomości E-mail lub alternatywny numer telefonu uwierzytelniania hello imieniu mojej użytkowników?**

  > **Odpowiedź:** nie jest to możliwe dzisiaj.
  >
  >
* **Pytanie: jak portalu rejestracji hello wiedzieć, który tooshow opcje Moi użytkownicy?**

  > **Odpowiedź:** portalu rejestracji resetowania haseł hello programu tylko pokazuje hello opcje, które zostały włączone dla użytkownika. Te opcje można znaleźć w obszarze hello sekcji zasady resetowania hasła użytkownika karta Konfigurowanie w katalogu. Na przykład oznacza to, że jeśli pytania zabezpieczające nie jest włączona, następnie użytkownicy nie są możliwe tooregister dla tej opcji.
  >
  >
* **Pytanie: Jeśli użytkownik jest uznawany zarejestrowane?**

  > **A:** użytkownik jest uznawany w zarejestrowany dla usługi SSPR, gdy zarejestrowanych co najmniej hello **liczbę metod wymagane tooreset** ustawioną w hello [portalu Azure](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Resetowanie hasła
* **Pytanie: jak długo powinna czekać tooreceive wiadomości e-mail, SMS lub połączeń telefonicznych z resetowania hasła?**

  > **Odpowiedź:** poczty E-mail, wiadomości SMS i połączeń telefonicznych powinno nastąpić w obszarze jedną minutę, z normalna sytuacja hello 5-20 sekund.
    >Jeśli w tym czasie nie jest wyświetlany hello powiadomień:
        > * Sprawdź folder wiadomości-śmieci.
        > * Sprawdź hello numer lub adres e-mail jest nawiązywane połączenie jest hello, co oczekiwane.
        > * Sprawdź, czy dane uwierzytelniania hello w katalogu hello jest poprawnie sformatowana.
                >     * Przykład: "+ 1 4255551234" lub "user@contoso.com"
  >
  >
* **Pytanie: jakie języki są obsługiwane przez resetowania hasła?**

  > **Odpowiedź:** hello resetowania hasła interfejsu użytkownika, wiadomości SMS i głosu wywołania są zlokalizowane w hello te same języki, które są obsługiwane w usłudze Office 365.
  >
  >
* **Karta na konfigurowanie Q: części środowisko resetowania hasła hello uzyskać marki, gdy ustawić organizacji znakowania w katalogu Moje?**

  > **Odpowiedź:** portal resetowania haseł hello pokazuje logo organizacji i pozwala hello tooconfigure kontakt e-mail administratora łącze toopoint tooa niestandardowych lub adres URL. Każdej wiadomości e-mail, które są wysyłane przez resetowania haseł obejmuje logo organizacji, kolory, nazwy w treści hello hello poczty e-mail i dostosować na podstawie nazwy.
  >
  >
* **Pytanie: jak Poinformuj użytkowników o tym, gdzie toogo tooreset swoje hasła?**

  > **A:** toohttps://passwordreset.microsoftonline.com Twojego użytkowników może wysyłać bezpośrednio lub polecić je tooclick hello **nie ma dostępu do konta łącze** na dowolnej pracy lub nauki strony logowania. Można również opublikować te linki użytkownicy tooyour łatwo dostępne miejsce.
  >
  >
* **Pytanie: czy można użyć tej strony z urządzenia przenośnego?**

  > **Odpowiedź:** tak, ta strona działa na urządzeniach przenośnych.
  >
  >
* **Pytanie: czy odblokowywanie kont z lokalnej usługi active directory są obsługiwane podczas użytkownikom resetowania swoich haseł w?**

  > **Odpowiedź:** tak, gdy użytkownik resetuje hasła i zapisywania zwrotnego haseł został wdrożony za pomocą usługi Azure AD Connect, konto użytkownika jest odblokowany automatycznie podczas resetowania hasła.
  >
  >
* **Pytanie: jak można zintegrować resetowania bezpośrednio do mojego użytkownika logowania środowisko pulpitu**

  > **Odpowiedź:** w przypadku klienta programu Azure AD Premium można zainstalować programu Microsoft Identity Manager bez ponoszenia dodatkowych kosztów i wdrożyć hello lokalnego hasła resetowania rozwiązania toomeet to wymaganie.
  >
  >
* **Pytanie: czy można ustawić pytania zabezpieczeń dla różnych ustawień regionalnych?**

  > **Odpowiedź:** nie jest to możliwe dzisiaj.
  >
  >
* **Pytanie: jak wiele pytań możemy skonfigurować dla opcji uwierzytelniania pytania zabezpieczające hello?**

  > **Odpowiedź:** too20 pytania zabezpieczające niestandardowych w hello skonfigurowaniem [portalu Azure](https://portal.azure.com).
  >
  >
* **Pytanie: jak długo może być pytania zabezpieczające?**

  > **Odpowiedź:** pytania zabezpieczające może mieć długość od 3 do 200 znaków.
  >
  >
* **Pytanie: jak długo może być toosecurity odpowiedzi na pytania?**

  > **Odpowiedź:** odpowiedzi może być 3 too40 znaków.
  >
  >
* **Pytanie: czy odrzucony zduplikowane odpowiedzi na pytania toosecurity?**

  > **Odpowiedź:** tak, możemy Odrzuć toosecurity zduplikowane odpowiedzi na pytania.
  >
  >
* **Pytanie: czy maja rejestru użytkownika hello tego samego pytanie zabezpieczające więcej niż raz?**

  > **Odpowiedź:** nie, gdy użytkownik rejestruje dane pytanie, ich nie może zarejestrować dla tego zapytania po raz drugi.
  >
  >
* **Pytanie: czy jest możliwe tooset minimalny limit pytania zabezpieczające w celu rejestracji i resetowania?**

  > **Odpowiedź:** tak, można ustawić limit jeden dla rejestracji i drugi dla resetowania. pytania zabezpieczające 3 – 5 może być wymagany w czasie rejestracji i 3 – 5 mogą być wymagane w celu resetowania.
  >
  >
* **Pytanie: Jeśli użytkownik został zarejestrowany w więcej niż maksymalna liczba pytań wymaganych tooreset hello, jak są pytania zabezpieczające wybrane podczas resetowania?**

  > **A:** zabezpieczeń N pytania są losowo wybrane poza hello łącznej liczby pytań, a użytkownik został zarejestrowany, gdzie N to hello **liczba pytań wymaganych tooreset**. Na przykład jeśli użytkownik ma 5 pytania zabezpieczające w zarejestrowany, ale tooreset wymagane są tylko 3, 3 hello 5 są wybierane losowo i przedstawionego na resetowanie. Jeśli hello użytkownik otrzymuje odpowiedzi hello pytania toohello niewłaściwy, procesu wyboru hello będzie się powtarzał atakowaniu pytanie tooprevent.
  >
  >
* **Pytanie: czy można uniemożliwić użytkownikom próby resetowania wielokrotnie w krótkim przedziale czasu?**

  > **Odpowiedź:** tak, są wbudowane w tooprotect resetowania hasła przed niewłaściwym użyciem funkcje zabezpieczeń. Użytkownicy mogą tylko spróbuj 5 próbach resetowania hasła w ciągu godziny przed jest zablokowane przez 24 godziny. Użytkownicy mogą tylko spróbuj toovalidate numeru telefonu, 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny. Użytkownicy mogą tylko spróbuj użyć metody pojedynczego uwierzytelniania 5 razy w ciągu godziny przed jest zablokowane przez 24 godziny.
  >
  >
* **Pytanie: na jak długo są prawidłowe hello poczty e-mail i SMS jednorazowy kod dostępu?**

  > **Odpowiedź:** hello okres istnienia sesji do resetowania hasła jest 105 minut. Od początku hello hello operacji resetowania hasła, hello użytkownika tooreset 105 minut swoje hasło. Witaj poczty e-mail i SMS jednorazowy kod dostępu są nieprawidłowe po tym okresie.
  >
  >

## <a name="password-change"></a>Zmienianie hasła
* **Pytanie: gdzie powinien Moi użytkownicy? toochange haseł**

  > **A:** użytkownicy mogą zmieniać swoje hasła dowolnym Zobacz ich obraz profilu lub ikonę (podobnie jak w hello prawym górnym rogu ich [usługi Office 365](https://portal.office.com) lub [panelu dostępu](https://myapps.microsoft.com) wykonywania. Użytkownicy mogą zmieniać swoje hasła z hello [strony panelu dostępu profilu](https://account.activedirectory.windowsazure.com/r#/profile). Użytkownicy mogą również być zadawane toochange haseł automatycznie ekranu logowania hello Azure AD, jeśli ich hasła wygasły. Ponadto użytkownicy mogą przechodzić toohello [Portal zmiany hasła programu Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) bezpośrednio próbujące toochange haseł.
  >
  >
* **Pytanie: czy Moi użytkownicy powiadamianych w portalu usługi Office hello po wygaśnięciu hasła lokalnego?**

  > **Odpowiedź:** jest to możliwe dzisiaj Jeśli używasz usług AD FS, wykonując instrukcje hello tutaj: [wysyłanie oświadczeń zasad haseł z usług AD FS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Jeśli używasz synchronizacji skrótu hasła nie jest to możliwe dzisiaj. Jest to spowodowane nie zsynchronizować zasad haseł z lokalnej, więc nie jest możliwe w firmie Microsoft napotyka toopost wygaśnięcia powiadomienia toocloud. W obu przypadkach możliwe jest również zbyt[Powiadom użytkowników, których hasła są o tooexpire przy użyciu programu PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Raporty zarządzania hasła
* **Pytanie: jak długo trwa dla danych tooshow się na raporty zarządzania hello hasło?**

  > **Odpowiedź:** danych powinny pojawiać się na raporty zarządzania hello hasła w ciągu 5 – 10 minut. Go niektórych wystąpień może trwać tooan tooappear godzinę.
  >
  >
* **Pytanie: jak można filtrować raporty zarządzania hello hasło?**

  > **Odpowiedź:** można filtrować raporty zarządzania hello hasło, klikając hello małych Lupa toohello extreme prawej hello etykiety kolumn, górze hello hello raportu. Jeśli chcesz bardziej zaawansowane funkcje filtrowania toodo, można pobrać hello tooexcel raportu i utworzyć tabelę przestawną.
  >
  >
* **Pytanie: jaka jest maksymalna liczba zdarzeń hello są przechowywane w raportach zarządzania hasło hello?**

  > **Odpowiedź:** się too75, 000 hasła resetowania lub hasło resetowania rejestracji zdarzenia są przechowywane w raporty zarządzania hasło hello spanning Utwórz kopię zapasową too30 dni.  Pracujemy nad tym tooexpand to numer tooinclude więcej zdarzeń.
  >
  >
* **Pytanie: jak daleko raporty zarządzania hasło hello go?**

  > **Odpowiedź:** zarządzania hasłami hello raporty operacji Pokaż występujących hello ostatnich 30 dni. Teraz Jeśli potrzebujesz tooarchive te dane, można pobrać raporty hello okresowo i zapisać je w innej lokalizacji.
  >
  >
* **Pytanie: istnieje już maksymalną liczbę wierszy, które mogą być wyświetlane w raportach zarządzania hasło hello?**

  > **Odpowiedź:** tak, maksymalnie 75,000 wierszy może pojawić się w zależności od hello raporty zarządzania hasło, czy są one wyświetlane w hello interfejsu użytkownika lub pobierania.
  >
  >
* **Pytanie: istnieje już tooaccess interfejsu API hello hasła resetowania lub rejestracji raportowania danych?**

  > **Odpowiedź:** tak, zobacz powitania po dokumentacji toolearn uzyskać dostęp hasła hello zresetować strumienia danych raportowania.  [Dowiedz się, jak tooaccess resetowania hasła zdarzeń do raportowania programowo](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Zapisywanie zwrotne haseł
* **Pytanie: jak działa funkcji zapisywania zwrotnego haseł w tle hello?**

  > **Odpowiedź:** zobacz [sposób działania funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md) dla wyjaśnienie, co się stanie po włączeniu funkcji zapisywania zwrotnego haseł i jak dane przepływają przez hello system wrócić do środowiska lokalnego.
  >
  >
* **Pytanie: jak długo funkcji zapisywania zwrotnego haseł trwa toowork?  Czy istnieje opóźnienie synchronizacji jak z synchronizacji skrótów haseł?**

  > **Odpowiedź:** błyskawicznych jest funkcji zapisywania zwrotnego haseł. Jest synchroniczne potok, który działa zasadniczo inaczej niż synchronizacji skrótu hasła. Zapisywanie zwrotne haseł umożliwia użytkownikom tooget w czasie rzeczywistym swoją opinię na temat powodzenia hello hasła Resetowanie lub zmienianie operacji. Średni czas pomyślnego funkcji zapisywania zwrotnego haseł Hello jest w obszarze 500 ms.
  >
  >
* **Pytanie: Jeśli konto lokalne jest wyłączone, Moje konto/dostęp do chmury wpływ?**

  > **Odpowiedź:** wyłączenie Identyfikatora lokalnej chmury również zostaną wyłączone identyfikator/access interwałem hello następnej synchronizacji za pomocą domyślnego byt AAD Connect to co 30 minut.
  >
  >
* **Pytanie: czy Moje konto lokalne jest ograniczane przez zasady haseł lokalnej usługi Active Directory, SSPR przestrzegać tych zasad po zmianie hasła hello?**

  > **Odpowiedź:** tak, zależy od usługi SSPR i przestrzega zasad hello lokalne zasady haseł AD, w tym typowych zasad haseł domeny AD, a także wszystkie zdefiniowane zasady haseł szczegółowe docelowe tooa danego użytkownika.
  >
  >
* **Pytanie: jakie typy kont zapisywania zwrotnego haseł działa dla?**

  > **Odpowiedź:** funkcji zapisywania zwrotnego haseł działa w przypadku federacyjnym i synchronizacji skrótów haseł użytkowników.
  >
  >
* **Pytanie: czy funkcji zapisywania zwrotnego haseł wymusić zasady haseł mojej domeny?**

  > **Odpowiedź:** tak, funkcję zapisywania zwrotnego haseł wymusza okres ważności hasła, historii złożoności, filtrów i inne ograniczenia, może umieścić w miejscu na haseł w domenie lokalnej.
  >
  >
* **Pytanie: czy jest bezpieczna funkcji zapisywania zwrotnego haseł?  Jak można mieć pewność, że I nie będzie włamania?**

  > **Odpowiedź:** tak, zapisywanie zwrotne haseł jest bezpieczne. tooread więcej informacji na temat hello cztery warstwy zabezpieczeń zaimplementowana przez usługę zapisywania zwrotnego haseł hello, zapoznaj się z hello [model zabezpieczeń zapisywania zwrotnego haseł](active-directory-passwords-writeback.md#password-writeback-security-model) sekcji w sposób działania funkcji zapisywania zwrotnego haseł.
  >
  >

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR
