---
title: "Szczegółowo: Azure AD SSPR | Dokumentacja firmy Microsoft"
description: "Azure AD samoobsługowego resetowania hasła nowości"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Samoobsługowe Resetowanie w usłudze Azure AD nowości haseł

Jak działa SSPR Co oznacza tej opcji w interfejsie hello? Kontynuuj czytanie toofind więcej informacji na temat usługi Azure AD samoobsługi hasła resetowania.

## <a name="how-does-hello-password-reset-portal-work"></a>Jak hasło hello zresetować portalu pracy

Gdy użytkownik nawiguje portalu resetowania haseł toohello, przepływu pracy zostało rozpoczęte toodetermine:

   * Jak można lokalizować z hello strony?
   * Witaj, konto użytkownika jest prawidłowy?
   * Jakie organizacji czy należy hello użytkownika?
   * Gdy hasło użytkownika hello jest zarządzany
   * Jest funkcja hello toouse licencjonowanych użytkowników hello?


Zapoznaj się z artykułem hello kroki toolearn o hello logiki stronę resetowania hasła hello.

1. Użytkownik klika polecenie hello nie może uzyskać dostępu połączenie z kontem lub gdy przechodzi on bezpośrednio za[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Oparte na powitania ustawienia regionalne przeglądarki hello środowisko jest renderowany w hello odpowiedni język. Witaj środowisko resetowania hasła jest zlokalizowana na te same języki Witaj, ponieważ obsługuje usługi Office 365.
3. Użytkownik wprowadza nazwę użytkownika i przekazuje captcha.
4. Usługi Azure AD sprawdza, czy użytkownika hello jest toouse stanie tę funkcję, wykonując następujące hello:
   * Sprawdza, czy ten użytkownik hello ma ta funkcja jest włączona i przypisanej licencji usługi Azure AD.
     * Jeśli użytkownik hello ma ta funkcja jest włączona lub przypisać licencję, użytkownik hello jest zadawane toocontact ich tooreset administratora swoje hasło.
   * Sprawdza, czy dane żądanie prawym hello zdefiniowane na koncie, zgodnie z zasadami administratora, które użytkownik hello ma.
     * Jeśli zasady wymaga tylko jedno żądanie, zapewnia się, że hello odpowiednie dane zdefiniowane dla co najmniej jednym z wyzwań hello włączane przez hello administrator zasad, które użytkownik hello ma.
       * Jeśli hello użytkownik nie jest skonfigurowany, a następnie hello użytkownika jest toocontact zaleca ich tooreset administratora swoje hasło.
     * Jeśli zasady hello wymaga dwóch wyzwania, następnie zapewnia się, że hello odpowiednie dane zdefiniowane dla co najmniej dwóch wyzwania hello włączane przez hello administrator zasad, które użytkownik hello ma.
       * Jeśli nie skonfigurowano hello użytkownika, a następnie firma Microsoft hello użytkownika jest toocontact zaleca ich tooreset administratora swoje hasło.
   * Sprawdza, czy hasło użytkownika hello odbywa się lokalnie (federacyjnych lub synchronizacji skrótów haseł).
     * Jeśli zapisywania zwrotnego jest wdrożone i hasło użytkownika hello odbywa się lokalnie, użytkownik hello jest dozwolone tooproceed tooauthenticate i resetowania hasła.
     * Jeśli zapisywania zwrotnego nie została wdrożona i hasło użytkownika hello odbywa się lokalnie, a następnie użytkownik hello jest zadawane toocontact ich tooreset administratora swoje hasło.
5. Jeśli okaże się, że użytkownik hello jest w stanie toosuccessfully zresetować swoje hasło, a następnie kieruje użytkownika hello hello proces resetowania.

## <a name="authentication-methods"></a>Metody uwierzytelniania

Po włączeniu funkcji samoobsługowego resetowania hasła (SSPR), musisz wybrać co najmniej jeden z hello następujące opcje dla metod uwierzytelniania. Zdecydowanie zaleca się wybranie co najmniej dwóch metod uwierzytelniania, dzięki czemu użytkownicy mają większą elastyczność.

* Adres e-mail
* Telefon komórkowy
* Telefon biurowy
* Pytania zabezpieczające

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Jakie pola są używane w katalogu hello danych uwierzytelniania

* Telefon biurowy odpowiada tooOffice telefonu
    * Użytkownicy są tooset nie można w tym polu samodzielnie, które muszą być zdefiniowane przez administratora
* Telefon komórkowy odpowiada tooeither numer telefonu uwierzytelniania (publicznie niewidoczny) lub telefonu komórkowego (widocznego publicznie)
    * usługi Hello najpierw szuka numer telefonu uwierzytelniania, następnie powraca tooMobile Phone Jeśli nie są zainstalowane
* Alternatywny adres E-mail odpowiada tooeither E-mail uwierzytelniania (publicznie niewidoczny) lub alternatywny adres E-mail
    * Usługa Hello najpierw szuka uwierzytelniania wiadomości E-mail, a następnie nie powiedzie się wstecz tooAlternate poczty E-mail

Domyślnie tylko atrybuty chmury hello, telefon biurowy i telefon komórkowy są synchronizowane tooyour katalogiem w chmurze z katalogu lokalnego dla danych uwierzytelniania.

Użytkownicy mogą tylko resetowania, hasła, gdy mają dane w metodach uwierzytelniania hello hello administrator jest włączona i wymaga.

Jeśli użytkownik nie ma ich toobe numer telefonu komórkowego widoczne w katalogu hello, lecz nadal jak toouse go do resetowania hasła, Administratorzy powinien nie wypełnić go w katalogu hello i hello użytkownik powinien wypełnij ich **numer telefonu uwierzytelniania**  atrybut za pośrednictwem hello [portalu rejestracji resetowania haseł](http://aka.ms/ssprsetup). Administratorzy mogą zobaczyć te informacje w profilu użytkownika hello, ale nie jest opublikowana w innym miejscu. Jeśli konto administratora Azure rejestruje numeru telefonu uwierzytelniania, są umieszczane w pole telefonu komórkowego hello i jest widoczny.

### <a name="number-of-authentication-methods-required"></a>Wiele metod uwierzytelniania wymagany

Ta opcja określa minimalną liczbę hello dostępne metody uwierzytelniania użytkownika musi przechodzić przez tooreset hello lub odblokowania hasła i można ustawić tooeither 1 lub 2.

Użytkownicy mogą wybierać z toosupply więcej metod uwierzytelniania, jeśli są one włączone przez administratora hello.

Jeśli użytkownik nie ma metody hello minimalne wymagane zarejestrowany, zobacz temat strona błędu, który kieruje toorequest tooreset administratora swoje hasło.

### <a name="how-secure-are-my-security-questions"></a>Jak bezpieczne czy moje pytania zabezpieczające

Jeśli używasz pytań zabezpieczających, zaleca się ich używany z innej metody jako może być mniej bezpieczne od innych metod, ponieważ niektóre osoby mogą dowiedzieć się odpowiedzi hello tooanother pytania użytkowników.

> [!NOTE] 
> Pytania zabezpieczające są przechowywane przez użytkowników i bezpiecznie obiektu użytkownika w katalogu hello i można tylko udzielane przez użytkowników podczas rejestracji. Nie istnieje sposób dla tooread administratora lub zmodyfikuj użytkowników pytań lub odpowiedzi.
>

### <a name="security-question-localization"></a>Lokalizacja pytanie zabezpieczeń

Wszystkie wstępnie zdefiniowanych pytania, które należy wykonać są zlokalizowane w hello pełny zestaw oparte na ustawienia regionalne przeglądarki użytkownika hello języków usługi Office 365.

* W jakim mieście poznałeś/poznałaś swoją pierwszą współmałżonkę lub partnerkę albo swojego pierwszego współmałżonka lub partnera?
* W jakim mieście spotkali się Twoi rodzice?
* Jakie jest najbliższe miasto, w którym mieszka Twoje rodzeństwo?
* W jakim mieście urodził się Twój ojciec?
* W jakim mieście podjąłeś/podjęłaś swoją pierwszą pracę?
* W jakim mieście urodziła się Twoja matka?
* W jakim mieście byłaś/eś w dniu Nowego Roku 2000?
* Co to jest hello nazwisko Twój ulubiony nauczyciel w dużej * służbowego?
* Co to jest nazwa hello uczelni, możesz zastosować toobut nie udało?
* Co to jest nazwa hello hello miejsca, w którym przechowywane są Twoje pierwsze wesele?
* Jak ma na drugie imię Twój ojciec?
* Jaka jest Twoja ulubiona potrawa?
* Jak ma na imię i nazwisko Twoja babcia od strony matki?
* Jakie jest drugie imię Twojej matki?
* Co to jest data urodzenia miesiąc i rok Twojego najstarszego rodzeństwa? (np. listopad 1985)
* Jak ma na drugie imię Twój najstarszy brat/siostra?
* Jak miał na imię i nazwisko Twój dziadek od strony ojca?
* Jakie jest drugie imię Twojego najmłodszego rodzeństwa?
* Jak nazywała się Twoja szkoła podstawowa?
* Co została po raz pierwszy hello i nazwisko Twój najlepszy przyjaciel w dzieciństwie?
* Co została po raz pierwszy hello i nazwisko Twoja pierwsza poważna sympatia?
* Jaki był hello nazwisko Twój ulubiony szkole nauczyciel?
* Jaki był hello marka i model Twojego pierwszego samochodu lub motocykla?
* Jaki był hello nazwę hello pierwszy Twoja Szkoła?
* Jaki był hello nazwę szpital Twoich hello, w którym narodzin?
* Jaki był hello nazwę ulicy hello Twój pierwszy dzieciństwa?
* Imię hello Twój bohater z dzieciństwa?
* Imię hello Twoja ulubiona maskotka?
* Imię hello Twoje pierwsze zwierzę domowe?
* Jaki był Twój pseudonim w dzieciństwie?
* Jaki był Twój ulubiony sport w szkole średniej?
* Jaka była Twoja pierwsza praca?
* Jakie były hello cztery ostatnie cyfry Twojego numeru telefonu z dzieciństwa?
* Dzieciństwie, kim chciałeś/chciałaś toobe gdy dorośniesz?
* Kto jest hello osoby Najpopularniejsza poznana możesz?

### <a name="custom-security-questions"></a>Pytania zabezpieczające niestandardowych

Pytania zabezpieczające niestandardowe nie są zlokalizowane dla różnych ustawień regionalnych. Wszystkie pytania niestandardowe są wyświetlane w hello tego samego języka są wprowadzane w interfejsie użytkownika administracyjnego hello nawet, jeśli ustawienia regionalne przeglądarki użytkownika hello jest inna. Jeśli potrzebujesz zlokalizowanych pytania, użyj hello wstępnie zdefiniowanych pytań.

Maksymalna długość Hello pytanie zabezpieczające niestandardowych jest 200 znaków.

### <a name="security-question-requirements"></a>Wymagania dotyczące pytanie zabezpieczeń

* Ograniczenie liczby znaków minimalna odpowiedzi jest 3 znaków
* Odpowiedzi maksymalny limit znaków wynosi 40 znaków
* Użytkownicy nie mógł odpowiedzieć na powitania sam pytanie więcej niż jeden raz
* Użytkownicy mogą nie zapewnić hello toomore niż jedno pytanie odpowiedzi na takie same
* Każdy zestaw znaków mogą być używane toodefine pytania i odpowiedzi, w tym znaków Unicode
* Witaj liczbę pytań zdefiniowanych przez musi być większa niż lub równa toohello liczba pytań wymaganych tooregister

## <a name="registration"></a>Rejestracja

### <a name="require-users-tooregister-when-signing-in"></a>Wymagaj tooregister użytkowników podczas logowania

Włączenie tej opcji wymaga użytkownika, który jest włączony dla hasła resetowania rejestracji resetowania haseł hello toocomplete, jeśli ich zalogować się przy użyciu usługi Azure AD toosign w takich jak te, które należy wykonać tooapplications:

* Office 365
* Azure Portal
* Panel dostępu
* Aplikacji federacyjnych
* Niestandardowe aplikacje przy użyciu usługi Azure AD

Wyłączenie tej funkcji zezwala użytkownikom toomanually rejestru informacje kontaktowe, odwiedzając [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) lub przez kliknięcie przycisku hello **zarejestrować do resetowania hasła** łącze pod hello Karta profil w panelu dostępu hello.

> [!NOTE]
> Użytkownicy można odrzucić portalu rejestracji resetowania haseł hello przez kliknięcie przycisku Anuluj lub zamknięcie okna hello, ale są monitowani o każdym razem, gdy są one logowania aż do chwili zakończenia rejestracji.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Liczba dni, zanim użytkownicy będą zadawane tooreconfirm ich informacje dotyczące uwierzytelniania

Ta opcja określa okres hello między ustawienie i reconfirming informacje dotyczące uwierzytelniania i jest dostępna tylko po włączeniu hello **wymagają tooregister użytkowników podczas logowania** opcji.

Prawidłowe wartości to 0 730 dni od 0, co oznacza nigdy nie pytaj użytkowników tooreconfirm ich informacje dotyczące uwierzytelniania

## <a name="notifications"></a>Powiadomienia

### <a name="notify-users-on-password-resets"></a>Czy powiadamiać użytkowników o resetowaniu hasła?

Jeśli ta opcja jest ustawiona tooyes, hello użytkownika, który jest zresetowania hasła otrzymuje wiadomość e-mail z informacją, że ich hasło zostało zmienione za pośrednictwem hello SSPR portalu tootheir podstawowy i alternatywny adres e-mail adresów w pliku w usłudze Azure AD. Żaden inny użytkownik jest powiadamiany o resetowania zdarzeń.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Powiadamianie wszystkich administratorów innych administratorów resetowanie haseł

Jeśli ta opcja jest ustawiona tooyes, następnie **wszystkich administratorów** odbierać poczty e-mail tootheir podstawowego adresu e-mail w pliku w usłudze Azure AD z informacją, że inny administrator zmienił ich hasła przy użyciu funkcji SSPR.

Przykład: Istnieją cztery Administratorzy w środowisku. Administrator "A" Resetuje hasła przy użyciu funkcji SSPR. Administratorzy B, C i D otrzymywać wiadomości e-mail powiadamiające ich sytuacja.

## <a name="on-premises-integration"></a>Integracja z lokalnymi

Jeśli masz zainstalowany, skonfigurowane i włączone Azure AD Connect masz dodatkowe opcje integracji z lokalnymi.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Zapisywania zwrotnego haseł tooyour lokalnego katalogu

Określa, czy włączono funkcję zapisywania zwrotnego haseł dla tego katalogu, a jeśli zapisywania zwrotnego jest włączona, wskazuje stan hello hello lokalną usługą zapisywania zwrotnego. Jest to przydatne, jeśli chcesz tootemporarily Wyłącz hello — zapisywanie zwrotne haseł, bez ponowne konfigurowanie usługi Azure AD Connect.

* Jeśli przełącznik hello jest tooyes zestaw funkcji zapisywania zwrotnego będzie włączona, a federacyjnych i hasło skrótu synchronizowane użytkownicy będą mogli tooreset haseł.
* Jeśli przełącznik hello jest toono zestaw funkcji zapisywania zwrotnego zostanie wyłączone, a federacyjnych i użytkowników synchronizacji skrótu hasła nie będą mogli tooreset haseł.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Zezwalaj użytkownikom toounlock kont bez potrzeby resetowania hasła

Określa, czy użytkownicy, którzy odwiedzają witrynę portalu resetowania haseł hello powinna być toounlock opcji hello danej usługi Active Directory ich lokalnych kont bez zresetowania hasła. Domyślnie usługi Azure AD będą zawsze odblokowania konta podczas resetowania hasła, to ustawienie pozwala tooseparate tych dwóch operacji. 

* Jeśli ustawiona zbyt "tak", użytkownicy będą hello danej opcji tooreset hasła i odblokowania konta hello lub toounlock bez potrzeby resetowania haseł hello.
* Jeśli ustawiona za "nie", a następnie użytkownicy będą mogli tooperform tylko resetowania hasła połączonych i konto operacji odblokowania.

## <a name="network-requirements"></a>Wymagania dotyczące sieci

### <a name="firewall-rules"></a>Reguły zapory

[Lista adresów IP i adresów URL programu Microsoft Office](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Azure AD Connect wersji 1.1.443.0 i nowszych możesz muszą wychodzącego następujące toohello dostępu protokołu HTTPS
* passwordreset.microsoftonline.com
* servicebus.Windows.NET

Bardziej szczegółowego dostępu można znaleźć listy hello zaktualizowane Microsoft Azure Datacenter zakresów adresów IP jest aktualizowane co środę i zaczęły obowiązywać hello następujące poniedziałek [tutaj](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Limity czasu bezczynności połączenia

Hello Azure AD Connect narzędzie wysyła tooensure punkty końcowe tooServiceBus okresowe polecenia ping/keepalives czy hello połączenie pozostaje aktywne. Powinien hello narzędzie wykrywa, że zbyt wiele połączeń są trwa skasowane, automatycznie zwiększa częstotliwość hello punktu końcowego toohello polecenia ping. Hello najniższy "Wyślij polecenie ping interwałów" porzucania toois 1 ping co 60 sekund, jednak zdecydowanie zalecamy, czy serwery proxy/zapory zezwalają toopersist bezczynności połączenia dla co najmniej 2 – 3 minuty. * Dla wcześniejszych wersji zalecamy czterech minut lub dłużej.

## <a name="active-directory-permissions"></a>Uprawnienia usługi Active Directory

Witaj konto określone w hello Azure AD Connect narzędzia musi mieć resetowania hasła, Zmień hasło na lockoutTime uprawnienia do zapisu i uprawnienia do zapisu na pwdLastSet rozszerzone prawa w obu obiektu głównego hello **każdej domeny** w tym lesie **lub** na powitania użytkownika jednostki organizacyjne mają toobe w zakresie dla usługi SSPR.

Jeśli nie masz pewności jakiego konta hello powyżej odwołuje się do Otwórz hello Azure Active Directory Connect konfiguracji interfejsu użytkownika i kliknij opcję hello widoku bieżącej konfiguracji. Konto Hello potrzebne toois uprawnienia tooadd kategorii "Katalogów synchronizowane"

Ustawienie tych uprawnień pozwala hello kontom usług ma każdego lasu haseł toomanage imieniu kont użytkownika w tym lesie. **Pominięcie tooassign tych uprawnień, następnie, mimo że zapisywania zwrotnego pojawia się toobe poprawnie skonfigurowane, użytkownicy wystąpiły błędy podczas próby toomanage ich hasłami lokalnymi z hello chmury.**

> [!NOTE]
> Może potrwać tooan godzinę lub dłużej dla tych obiektów tooall tooreplicate uprawnienia w katalogu.
>

tooset hello ustawienia odpowiednie dla toooccur zapisywania zwrotnego haseł

1. Otwórz przystawkę Użytkownicy usługi Active Directory i komputery z konta, które ma uprawnienia administratora w odpowiedniej domenie hello
2. W menu Widok hello upewnij się, że jest włączone funkcje zaawansowane
3. W lewym panelu hello kliknij prawym przyciskiem myszy obiekt hello, który reprezentuje katalog główny domeny hello hello i wybierz polecenie Właściwości
    * Kliknij kartę Zabezpieczenia hello
    * Następnie kliknij przycisk Zaawansowane.
4. Na karcie uprawnienia hello kliknij przycisk Dodaj
5. Wybierz konto hello czy uprawnienia są stosowane za (z konfiguracji usługi Azure AD Connect)
6. Wybierz obiekty potomne użytkownika toodrop stosuje hello rozwijane
7. W obszarze uprawnienia pola hello następującego hello wyboru
    * Hasło nie wygasa
    * Resetowanie hasła
    * Zmień hasło
    * Zapis lockoutTime
    * Zapis pwdLastSet
8. Kliknij przycisk Zastosuj/OK za pośrednictwem tooapply i zamknij wszystkie otwarte okna dialogowe.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Jak hasło zresetować pracy B2B użytkowników?
Resetowanie hasła i zmiany są w pełni obsługiwane we wszystkich konfiguracjach B2B.  Przeczytaj poniższe hello trzy jawne B2B przypadkach obsługiwana przez resetowania hasła.

1. **Użytkownicy z organizacji partnera, z istniejącą dzierżawą usługi Azure AD** — Jeśli w organizacji hello są partnerstwo z istniejącą dzierżawą usługi Azure AD, firma Microsoft **przestrzegać niezależnie od zasady resetowania hasła są włączone w tej dzierżawie**. Hasło zresetować toowork hello partnera organizacji potrzeb tylko toomake czy włączono usługi Azure AD SSPR, który jest bezpłatne dla klientów usługi Office 365, i może być włączona po hello czynnościach w ramach naszych [wprowadzenie do zarządzania hasłami ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) przewodnik.
2. **Użytkownicy, którzy konta, za pomocą [samoobsługowego tworzenia konta](active-directory-self-service-signup.md)**  — Jeśli organizacja hello są partnerstwo z używane hello [samoobsługowego tworzenia konta](active-directory-self-service-signup.md) tooget funkcji do dzierżawcy, nie możemy udostępnić je zresetowana z zastosowaniem Witaj poczty e-mail one zarejestrowane.
3. **Użytkownicy B2B** -żadnych nowych użytkowników B2B utworzone za pomocą nowego hello [możliwości B2B usługi Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md) będzie również stanie tooreset haseł z poczty e-mail hello one zarejestrowane podczas procesu zaproszenia hello.

tootest tego toohttp://passwordreset.microsoftonline.com wybierz jeden z tych użytkowników z firm partnerskich. Tak długo, jak długo mają alternatywny adres e-mail lub uwierzytelniania wiadomości e-mail zdefiniowanych resetowania haseł działa zgodnie z oczekiwaniami.

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Zasady**](active-directory-passwords-policy.md) — Omówienie zasad haseł usługi Azure AD i ich ustawianie
* [**Zapisywanie zwrotne haseł**](active-directory-passwords-writeback.md) — Jak zapisywanie zwrotne haseł współpracuje z katalogiem lokalnym
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

