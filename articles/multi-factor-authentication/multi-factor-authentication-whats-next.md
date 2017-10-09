---
title: "aaaConfigure usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strona, która opisuje jakie toodo obok za pomocą usługi MFA.  W tym raporty, oszustwa, jednorazowe obejście, niestandardowe wiadomości głosowe, buforowanie zaufanych adresów IP i aplikacji hasła."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: 7f6d0b0975a2c1da2de9b52e978b84475c79b218
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Konfigurowanie ustawień usługi Azure Multi-Factor Authentication
Ten artykuł ułatwia zarządzanie Azure Multi-Factor Authentication, skoro masz działa prawidłowo.  Obejmuje ona różne tematy ułatwiające hello tooget maksymalne wykorzystanie możliwości usługi Azure Multi-Factor Authentication.  Nie wszystkie te funkcje są dostępne w każdej wersji Azure Multi-Factor Authentication.

| Funkcja | Opis | 
|:--- |:--- |
| [Alert o oszustwie](#fraud-alert) |Alert o oszustwie można konfigurować i skonfigurować, aby użytkownicy mogą raportować tooaccess fałszywych prób ich zasobów. |
| [Jednorazowe obejście](#one-time-bypass) |Jednorazowe obejście pozwala tooauthenticate użytkownika jeden raz pomijając"" uwierzytelnianie wieloskładnikowe. |
| [Niestandardowe wiadomości głosowe](#custom-voice-messages) |Niestandardowe wiadomości głosowe pozwalają toouse własnych nagrań lub pozdrowienia przy użyciu uwierzytelniania wieloskładnikowego. |
| [Buforowanie](#caching-in-azure-multi-factor-authentication) |Buforowanie pozwala tooset w określonym przedziale czasu, aby kolejne próby uwierzytelniania powiedzie się automatycznie. |
| [Listę zaufanych adresów IP](#trusted-ips) |Administratorzy dzierżawy zarządzane lub federacyjnych służy weryfikacji dwuetapowej toobypass zaufanych adresów IP dla użytkowników, którzy zalogować się w firmie hello lokalny intranet. |
| [Hasła aplikacji](#app-passwords) |Hasła aplikacji umożliwia aplikacji, która nie jest uwierzytelnianie wieloskładnikowe toobypass obsługujący uwierzytelnianie wieloskładnikowe i kontynuować pracę. |
| [Zapamiętać usługi Multi-Factor Authentication na zapamiętanych urządzeniach i przeglądarki](#remember-multi-factor-authentication-for-devices-that-users-trust) |Umożliwia tooremember urządzeń przez liczbę dni, po użytkownik pomyślnie zalogował się przy użyciu usługi MFA. |
| [Metody wyboru weryfikacji](#selectable-verification-methods) |Zapewnia metody uwierzytelniania hello toochoose, które są dostępne dla użytkowników toouse. |

## <a name="access-hello-azure-mfa-management-portal"></a>Witaj dostęp do portalu zarządzania Azure MFA

Funkcje Hello omówione w tym artykule są konfigurowane w hello portalu zarządzania Azure Multi-Factor Authentication. Istnieją dwa sposoby tooaccess hello portalu zarządzania usługi MFA za pośrednictwem hello klasycznego portalu Azure. najpierw Hello jest zarządzanie dostawcy uwierzytelniania wieloskładnikowego. Hello jest drugi za pomocą ustawień usługi MFA hello. 

### <a name="use-an-auth-provider"></a>Użyj dostawcy uwierzytelniania

Jeśli używasz dostawcy uwierzytelniania wieloskładnikowego na podstawie zużycia MFA, za pomocą tego portalu zarządzania hello tooaccess — metoda.

tooaccess hello portalu zarządzania usługi MFA za pomocą dostawcy usługi Azure Multi-Factor Authentication, logowanie na powitania klasycznego portalu Azure jako administrator, a hello wybierz opcję Active Directory. Kliknij przycisk hello **dostawców uwierzytelniania wieloskładnikowego** , a następnie wybierz swój katalog a kliknij hello **Zarządzaj** u dołu hello.

### <a name="use-hello-mfa-service-settings-page"></a>Strona Ustawienia usługi MFA hello 

Jeśli dostawca uwierzytelniania MFA lub Azure MFA, Azure AD Premium lub Enterprise Mobility + Security licencji, użyj tej strony metody tooaccess hello MFA usługi ustawień.

tooaccess hello portalu zarządzania usługi MFA za pośrednictwem hello strony ustawień usługi MFA, zaloguj się do klasycznego portalu Azure jako administrator hello i wybierz opcję Active Directory hello. Kliknij polecenie w katalogu, a następnie kliknij przycisk hello **Konfiguruj** kartę. W sekcji uwierzytelnianie wieloskładnikowe hello, wybierz **Zarządzaj ustawieniami usługi**. U dołu hello hello ustawienia usługi MFA strony, kliknij przycisk hello **portal toohello Przejdź** łącza.


## <a name="fraud-alert"></a>Alert o oszustwie
Alert o oszustwie można konfigurować i skonfigurować, aby użytkownicy mogą raportować tooaccess fałszywych prób ich zasobów.  Użytkownicy mogą raportować oszustwa z aplikacją mobilną hello lub przez telefon.

### <a name="set-up-fraud-alert"></a>Konfigurowanie oszustwa
1. Przejdź toohello portalu zarządzania usługi MFA, zgodnie z instrukcjami hello hello początku tej strony.
2. W portalu zarządzania Azure Multi-Factor Authentication hello, kliknij przycisk **ustawienia** w obszarze hello sekcji konfiguracji.
3. W obszarze hello alarm oszustwa części strony ustawień hello, sprawdź hello **użytkownicy alertów oszustwa toosubmit** wyboru.
4. Wybierz **zapisać** tooapply zmiany. 

### <a name="configuration-options"></a>Opcje konfiguracji

- **Blokuj użytkownika, gdy zostaje zgłoszone oszustwo** — Jeśli oszustwa raporty użytkownika, jego konta jest zablokowane.
- **Kod oszustwa podczas początkowego pozdrowienia tooReport** -użytkowników zwykle naciśnij klawisz # tooconfirm funkcja weryfikacji dwuetapowej. Jeśli chcą oszustwa tooreport one wprowadzić kod przed naciśnięciem przycisku #. Ten kod jest **0** domyślnie, ale można go dostosować.

> [!NOTE]
> Pozdrowienia głosowe domyślna firmy Microsoft, poinstruuj użytkowników toopress 0# toosubmit alarm oszustwa. Jeśli chcesz toouse kodu innego niż 0, należy zarejestrować i przekaż własne niestandardowe pozdrowienia głosowe odpowiednie instrukcje.

![Opcje alertów oszustwa — zrzut ekranu](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Jak użytkownicy zgłosić oszustwo 
Alert o oszustwie mogą być zgłaszane na dwa sposoby.  Albo za pomocą aplikacji mobilnej hello za pośrednictwem telefonu hello.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Zgłoś oszustwo z aplikacją mobilną hello
1. Po wysłaniu tooyour phone weryfikacji zaznacz go aplikacji Microsoft Authenticator hello tooopen.
2. Wybierz **Odmów** na powitania powiadomień. 
3. Wybierz **zgłoszenia oszustwa**.
4. Aplikacja hello Zamknij.

#### <a name="report-fraud-with-a-phone"></a>Zgłoś oszustwo przy użyciu telefonu
1. Gdy połączenie weryfikacyjne w tooyour telefonu, udzielenie odpowiedzi.  
2. tooreport oszustwa, wprowadź kod oszustwa hello (wartość domyślna to 0) i następnie hello znak #. Otrzymasz powiadomienie alarm oszustwa zostało przesłane.
3. Wywołanie hello zakończenia.

### <a name="view-fraud-reports"></a>Wyświetl raporty dotyczące oszustwa
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Po lewej stronie powitania wybierz usługę Active Directory.
3. Na górnym umożliwia hello **dostawców uwierzytelniania wieloskładnikowego**. Spowoduje to wyświetlenie listy dostawców uwierzytelniania wieloskładnikowego.
4. Wybierz dostawcę uwierzytelniania wieloskładnikowego, a następnie kliknij przycisk **Zarządzaj** u dołu hello hello strony. Otwiera Hello portalu zarządzania Azure Multi-Factor Authentication.
5. Na powitania usługi Multi-Factor Authentication portalu zarządzania Azure, w obszarze Wyświetl raport, kliknij przycisk **alarm oszustwa**.
6. Określ zakres dat hello ma tooview hello raportu. Można również określić nazwy użytkowników, numerów telefonów i stan hello użytkownika.
7. Kliknij pozycję **Run** (Uruchom). Spowoduje to wyświetlenie raportu alertów oszustwa. Kliknij przycisk **wyeksportować tooCSV** w razie potrzeby tooexport hello raportu.

## <a name="one-time-bypass"></a>Jednorazowe obejście
Jednorazowe obejście pozwala tooauthenticate użytkownika jeden raz bez przeprowadzania weryfikacji dwuetapowej. Witaj obejście jest tymczasowe i wygasa po określonym czasie. W sytuacjach, gdzie hello aplikacji mobilnej lub telefon nie odbiera powiadomienia lub połączeń telefonicznych można włączyć jednorazowe obejście tak hello użytkownik może uzyskać dostęp hello żądanego zasobu.

### <a name="create-a-one-time-bypass"></a>Utwórz jednorazowe obejście
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź toohello portalu zarządzania usługi MFA, zgodnie z instrukcjami hello hello początku tej strony.
3. W portalu zarządzania Azure Multi-Factor Authentication hello, jeśli zostanie wyświetlony na powitania nazwę dzierżawcy lub dostawcy usługi Azure MFA hello pozostawione z  **+**  dalej tooit kliknij hello  **+**  Zobacz różnych grup replikacji serwera usługi MFA a hello Azure Default. Wybierz odpowiednią grupę hello.
4. W obszarze Administracja użytkownika, wybierz **jednorazowe obejście**.
5. Na stronie jednorazowe obejście powitania kliknij **nowe jednorazowe obejście**.

  ![Chmura](./media/multi-factor-authentication-whats-next/create1.png)

6. Wprowadź nazwę użytkownika hello, hello liczbę sekund obejścia hello istnieje, a hello przyczynę obejścia hello. Kliknij przycisk **obejścia**.
7. Witaj limit czasu przechodzi w stan obowiązywać natychmiast, tak użytkownika hello toosign potrzeb w przed hello jednorazowe obejście wygaśnie. 

### <a name="view-hello-one-time-bypass-report"></a>Widok hello jednorazowe obejście raportu
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Po lewej stronie powitania wybierz usługę Active Directory.
3. Na górnym umożliwia hello **dostawców uwierzytelniania wieloskładnikowego**. Spowoduje to wyświetlenie listy dostawców uwierzytelniania wieloskładnikowego.
4. Wybierz dostawcę uwierzytelniania wieloskładnikowego, a następnie kliknij przycisk **Zarządzaj** u dołu hello hello strony. Otwiera Hello portalu zarządzania Azure Multi-Factor Authentication.
5. Na powitania portalu zarządzania Azure Multi-Factor Authentication, powitania po lewej stronie, w obszarze Wyświetl raport, kliknij przycisk **jednorazowe obejście**.
6. Określ zakres dat hello ma tooview hello raportu. Można również określić nazwy użytkowników, numerów telefonów i stan hello użytkownika.
7. Kliknij pozycję **Run** (Uruchom). Spowoduje to wyświetlenie raportu obejścia. Kliknij przycisk **wyeksportować tooCSV** w razie potrzeby tooexport hello raportu.

## <a name="custom-voice-messages"></a>Niestandardowe wiadomości głosowe
Niestandardowe wiadomości głosowe pozwalają toouse własnych nagrań lub pozdrowienia na potrzeby weryfikacji dwuetapowej. Mogą być one używane w dodanie tooor tooreplace hello Microsoft rekordów.

Przed rozpoczęciem należy pamiętać o następujących hello:

* Witaj obsługiwane formaty plików są .wav lub .mp3.
* limit rozmiaru pliku Hello to 5 MB.
* Uwierzytelnianie wiadomości powinien być krótszy niż 20 sekund. Cokolwiek dłużej, niż może to spowodować hello toofail weryfikacji, ponieważ hello użytkownika może nie odpowiadać przed tootime zakończeniu powoduje wiadomość hello weryfikacji hello limit.

### <a name="set-up-a-custom-message"></a>Konfigurowanie niestandardowych komunikatów

Istnieją dwa toocreating części wiadomości niestandardowych. Najpierw przekazać wiadomość hello, a następnie włączenie go dla użytkowników.

tooupload wiadomości niestandardowych:

1. Tworzenie wiadomości głosowej niestandardowych przy użyciu jednej z hello obsługiwane formaty plików.
2. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
3. Przejdź toohello portalu zarządzania usługi MFA, zgodnie z instrukcjami hello hello początku tej strony.
4. W portalu zarządzania Azure Multi-Factor Authentication hello, kliknij przycisk **wiadomości głosowe** w obszarze hello sekcji konfiguracji.
5. Na powitania Konfiguruj: strona wiadomości głosowych, kliknij przycisk **nowej wiadomości głosowej**.
   ![Chmura](./media/multi-factor-authentication-whats-next/custom1.png)
6. Na powitania Konfiguruj: nowej wiadomości głosowej strony, kliknij przycisk **zarządzania plikami dźwięk**.
   ![Chmura](./media/multi-factor-authentication-whats-next/custom2.png)
7. Na powitania Konfiguruj: strona pliki dźwiękowe, kliknij przycisk **przekazać plik dźwiękowy**.
   ![Chmura](./media/multi-factor-authentication-whats-next/custom3.png)
8. Na powitania Konfiguruj: Przekaż plik dźwiękowy, kliknij przycisk **Przeglądaj** i przejdź wiadomości głosowej tooyour, kliknij przycisk **Otwórz**.
9. Dodaj opis, a następnie kliknij przycisk **przekazać**.
10. Po zakończeniu tego procesu, wyświetli się komunikat potwierdzający został pomyślnie przesłany plik hello.

tooturn wiadomości powitania na dla użytkowników:

1. Powitania po lewej stronie, kliknij przycisk **wiadomości głosowe**.
2. W obszarze hello sekcji wiadomości głosowe, kliknij **nowej wiadomości głosowej**.
3. Wybierz język z hello języka rozwinięcia.
4. Jeśli ten komunikat jest dla określonej aplikacji, określ wartość w pole aplikacji hello.
5. Z listy rozwijanej Typ wiadomość hello wybierz toobe typu wiadomość hello zastąpiona przez nowe wiadomości niestandardowych.
6. Z hello plik dźwiękowy listy rozwijanej wybierz plik dźwiękowy hello, który został przekazany w pierwszej części hello.
7. Kliknij przycisk **Utwórz**. Komunikat potwierdza, że pomyślnie utworzono wiadomości głosowej.
    ![Chmura](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Buforowanie w uwierzytelnianie wieloskładnikowe platformy Azure
Buforowanie pozwala tooset w określonym przedziale czasu, aby automatycznie powiedzie się kolejne próby uwierzytelniania w tym przedziale czasu. Służy to głównie systemów lokalnych, takich jak VPN wysyłania wielu żądań weryfikacji podczas pierwszego żądania hello jest nadal w toku. Dzięki temu toosucceed kolejnych żądań hello automatycznie po hello użytkownika powiedzie się hello pierwszy Weryfikacja w toku. 

Buforowanie nie jest zamierzone toobe używane do logowania tooAzure AD.

### <a name="set-up-caching"></a>Konfigurowanie pamięci podręcznej 
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź toohello portalu zarządzania usługi MFA, zgodnie z instrukcjami hello hello początku tej strony.
3. W portalu zarządzania Azure Multi-Factor Authentication hello, kliknij przycisk **buforowanie** w obszarze hello sekcji konfiguracji.
4. Na powitania Konfiguruj buforowanie strony kliknij **nową pamięć podręczną**.
5. Wybierz typ pamięci podręcznej hello i hello sekund buforowania. Kliknij przycisk **Utwórz**.

<center>![Chmura](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>Zaufane adresy IP
Listę zaufanych adresów IP to funkcja usługi Azure MFA, używaną przez administratorów dzierżawy zarządzane lub federacyjnych toobypass weryfikacji dwuetapowej dla użytkowników, którzy są logujący się z firmy hello lokalny intranet. Ta funkcja jest dostępna z pełną wersją hello Azure Multi-Factor Authentication, hello bezpłatną wersję dla administratorów. Aby uzyskać szczegółowe informacje o sposobie tooget hello pełną wersję programu Azure Multi-Factor Authentication, zobacz [Azure Multi-Factor Authentication](multi-factor-authentication.md).

| Typ dzierżawy usługi Azure AD | Dostępne opcje zaufany adres IP |
|:--- |:--- |
| Zarządzane |<li>Określonych zakresów adresów IP — Administratorzy mogą określić zakres adresów IP, które można pominąć weryfikacji dwuetapowej dla użytkowników, którzy są podpisywania intranecie firmy hello.</li> |
| Federacyjna |<li>Wszyscy użytkownicy federacyjnym — federacyjnych wszystkich użytkowników, którzy są podpisywania w z wewnątrz hello organizacji będzie pominąć weryfikacji dwuetapowej przy użyciu oświadczenia wydane przez usługi AD FS.</li><br><li>Określonych zakresów adresów IP — Administratorzy mogą określić zakres adresów IP, które można pominąć weryfikacji dwuetapowej dla użytkowników, którzy są podpisywania intranecie firmy hello. |

To obejście działa tylko z wewnątrz sieci intranet firmy. Na przykład jeśli wybrano federacyjnych wszystkich użytkowników, a użytkownik loguje się z intranetu hello firmy zewnętrznej, które użytkownik ma tooauthenticate przy użyciu weryfikacji dwuetapowej, nawet jeśli użytkownik hello przedstawia oświadczenia usług AD FS. 

**Środowisko użytkownika końcowego w sieci corpnet:**

Po wyłączeniu zaufanych adresów IP weryfikacji dwuetapowej jest wymagane dla przepływów przeglądarki, a hasła aplikacji są wymagane dla starszych aplikacji wzbogaconego klienta. 

Po włączeniu zaufanych adresów IP, weryfikacja dwuetapowa to *nie* wymagane dla przepływów przeglądarki, a następnie hasła aplikacji są *nie* wymagane starszych aplikacji wzbogaconego klienta, pod warunkiem, że hello użytkownika nie już utworzyła hasła aplikacji. Po użyciu hasła aplikacji jest używany, pozostaje wymagane. 

**Corpnet poza środowisko użytkownika końcowego:**

Czy zaufanych adresów IP jest włączone, weryfikacja dwuetapowa jest wymagane dla przepływów przeglądarki, a hasła aplikacji są wymagane dla starszych aplikacji wzbogaconego klienta. 

### <a name="tooenable-trusted-ips"></a>tooenable zaufanych adresów IP
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź na stronie ustawień usługi MFA toohello zgodnie z instrukcjami hello na początku hello tego artykułu.
3. Na stronie ustawień usługi hello w obszarze zaufanych adresów IP dostępne są dwie opcje:
   
   * **Żądania od użytkowników federacyjnych pochodzące z moim intranecie** — Witaj zaznaczenie. Wszystkich użytkowników federacyjnych zalogowanych z sieci firmowej hello będzie pominąć weryfikacji dwuetapowej przy użyciu oświadczenia wydane przez usługi AD FS.
   * **Dla żądań z określonego zakresu publicznych adresów IP** — wprowadź hello adresów IP w polu tekstowym hello realizowane przy użyciu notacji CIDR. Na przykład: xxx.xxx.xxx.0/24 dla adresów IP xxx.xxx.xxx.1 zakresu hello — xxx.xxx.xxx.254 lub xxx.xxx.xxx.xxx/32 dla jednego adresu IP. Można wprowadzić się zakresów adresów IP too50. Użytkownicy, którzy zalogować się w tych adresów IP pominąć weryfikacji dwuetapowej.
4. Kliknij pozycję **Zapisz**.
5. Po zastosowaniu aktualizacji powitania kliknij **Zamknij**.

![Zaufane adresy IP](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Hasła aplikacji
Niektóre aplikacje, takich jak pakiet Office 2010 lub starszy i Apple Mail nie obsługują weryfikacji dwuetapowej. Nie są skonfigurowane tooaccept drugi weryfikacji. toouse tych aplikacji, należy toouse "haseł aplikacji" zamiast tradycyjnych hasła. hasła aplikacji Hello umożliwia toobypass aplikacji hello weryfikacji dwuetapowej i kontynuować pracę.

> [!NOTE]
> Nowoczesne uwierzytelnianie dla hello klientom pakietu Office 2013
> 
> Klienci Office 2013 (w tym programu Outlook) i nowszych protokołów nowoczesnego uwierzytelniania pomocy technicznej i może być włączone toowork w trakcie weryfikacji dwuetapowej. Po włączeniu hasła aplikacji nie są wymagane dla tych klientów.  Aby uzyskać więcej informacji, zobacz [pakietu Office 2013 nowoczesnego uwierzytelniania anonsowania publicznej wersji](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Tooknow ważne zagadnienia dotyczące haseł aplikacji
Oto Hello ważne listę rzeczy, które należy poznać dotyczące haseł aplikacji.

* Hasła aplikacji wystarcza tylko toobe wprowadzona po każdej aplikacji. Użytkownicy nie mają ścieżki tookeep z nich i wprowadzić je za każdym razem.
* Hello rzeczywiste hasło jest generowane automatycznie i nie został dostarczony przez użytkownika hello. Jest to spowodowane hasło generowane automatycznie hello jest trudniej tooguess atakująca i większe bezpieczeństwo.
* Istnieje limit 40 haseł na użytkownika. 
* Aplikacje, których buforowanie haseł i używać jej w scenariuszach lokalnych może rozpocząć się niepowodzeniem, ponieważ hasło aplikacji hello nie jest znana poza hello identyfikatora organizacyjnego. Przykładem jest wiadomości e-mail programu Exchange, które są lokalne, ale wiadomości powitania zarchiwizowane znajduje się w chmurze hello. Witaj tego samego hasła nie działa.
* Włączenie uwierzytelniania wieloskładnikowego na koncie użytkownika, hasła aplikacji mogą być używane z większości klientów korzystających z przeglądarki, takich jak Outlook i Lync, ale nie można wykonać działania administracyjne, przy użyciu hasła aplikacji za pomocą aplikacji korzystających z przeglądarki, takich jak Windows Nawet jeśli użytkownik ma konto administracyjne programu PowerShell.  Upewnij się, możesz utworzyć konto usługi za pomocą skryptów środowiska PowerShell toorun silnego hasła i nie należy włączać tego konta na potrzeby weryfikacji dwuetapowej.

> [!WARNING]
> Hasła aplikacji nie działają w środowiskach hybrydowych, w którym klienci komunikować się z lokalnie i w chmurze punkty końcowe wykrywania automatycznego. Jest to spowodowane hasła domeny są wymagane tooauthenticate lokalnymi i hasła aplikacji są wymagane tooauthenticate hello chmury.

### <a name="naming-guidance-for-app-passwords"></a>Wskazówki dotyczące haseł aplikacji nazewnictwa
Nazwy haseł aplikacji odzwierciedlały urządzenie hello, na którym są używane. Na przykład, jeśli użytkownik ma komputer przenośny z zainstalowanymi aplikacji korzystających z przeglądarki, takich jak Outlook, Word i Excel, utworzyć hasło aplikacji o nazwie komputer przenośny i użyć tego hasła aplikacji w tych aplikacjach. Następnie należy utworzyć inny hasło aplikacji o nazwie pulpitu hello tych samych aplikacji na komputerze stacjonarnym. 

Firma Microsoft zaleca utworzenie jednego hasła aplikacji na urządzenie, nie jednego hasła aplikacji na aplikację.

### <a name="federated-sso-app-passwords"></a>Hasła aplikacji federacyjnych (SSO)
Usługi Azure AD obsługuje Federacji (logowanie jednokrotne) z lokalnego systemu Windows serwera usług domenowych Active Directory (AD DS). Jeśli Twoja organizacja jest Sfederowane przy użyciu usługi Azure AD i będą toobe przy użyciu usługi Azure Multi-Factor Authentication, następnie hello następujące informacje dotyczące haseł aplikacji jest ważne. Ta sekcja dotyczy tylko klientów toofederated (rejestracji jednokrotnej SSO).

* Hasła aplikacji są weryfikowane przez usługę Azure AD i w związku z tym obejście federacji. Federacyjnej jest aktywnie stosowana tylko podczas konfigurowania haseł aplikacji.
* Dla użytkowników federacyjnych (SSO) firma Microsoft nigdy nie przechodź toohello dostawcy tożsamości (IdP) inaczej niż w przypadku przepływu pasywnego hello. Witaj hasła są przechowywane w hello identyfikatora organizacyjnego. Jeśli hello użytkownik opuści firmę hello, że informacje o identyfikatorze tooflow tooorganizational przy użyciu narzędzia DirSync w czasie rzeczywistym. Wyłączenie/usunięcie konta może trwać toosync godziny toothree, opóźnienie wyłączenia/usunięcia hasła aplikacji w usłudze Azure AD.
* Ustawienia lokalnej kontroli dostępu klienta nie są uznawane przez hasło aplikacji.
* Bez uwierzytelniania lokalnego możliwości rejestrowania/inspekcji jest dostępna dla hasła aplikacji.
* Niektórych zaawansowanych rozwiązań architektury może wymagać kombinację organizacji nazwy użytkownika i hasła i haseł aplikacji, podczas klientom, w zależności od tego, gdzie uwierzytelniania przy użyciu weryfikacji dwuetapowej. Dla klientów, którzy uwierzytelniania względem infrastruktury lokalnej użyje organizacyjnej nazwy użytkownika i hasła. Dla klientów, którzy uwierzytelniania usługi Azure AD należy użyć hasła aplikacji hello.

  Na przykład załóżmy, że masz architekturę, która składa się z następujących hello:

  * Federacji lokalnego wystąpienia usługi Active Directory z usługą Azure AD
  * Korzystasz z usługi Exchange online
  * W przypadku korzystania z Lync, będący w szczególności lokalnego
  * Używasz usługi Azure Multi-Factor Authentication

  ![Biurowego](./media/multi-factor-authentication-whats-next/federated.png)

  W takich przypadkach należy wykonać następujące hello:

  * Podczas podpisywania — w tooLync, użyj nazwy użytkownika i hasła Twojej organizacji.
  * Podczas próby książki adresowej hello tooaccess za pomocą klienta programu Outlook, który łączy tooExchange w trybie online, należy użyć hasła aplikacji.

### <a name="allow-app-password-creation"></a>Zezwalaj na tworzenie haseł aplikacji
Domyślnie użytkownicy nie mogą tworzyć hasła aplikacji. Ta funkcja musi być włączona. Użytkownicy tooallow hello hasła aplikacji toocreate możliwości, skorzystaj z hello następujące procedury:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź na stronie ustawień usługi MFA toohello zgodnie z instrukcjami hello na początku hello tego artykułu.
3. Zaznacz przycisk radiowy hello obok zbyt**Zezwalaj toosign hasła aplikacji toocreate użytkowników do aplikacji niekorzystających z przeglądarki**.

![Tworzenie haseł aplikacji](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Tworzenie haseł aplikacji
Użytkownicy mogą tworzyć hasła aplikacji podczas ich początkowe rejestracyjny. Otrzymują one opcję na końcu hello hello procesu rejestracji, która pozwala toocreate hasła aplikacji.

Użytkownicy mogą także tworzyć hasła aplikacji po zarejestrowaniu, zmieniając ich ustawień w portalu usługi Office 365 portalu lub hello Azure hello. Aby uzyskać więcej informacji i uzyskać szczegółowe instrukcje dla użytkowników, zobacz [co to są hasła aplikacji w usłudze Azure Multi-Factor Authentication](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Należy pamiętać, uwierzytelnianie wieloskładnikowe dla użytkowników zaufanych urządzeniach
Zapamiętywanie uwierzytelniania wieloskładnikowego dla urządzeń i przeglądarki czy zaufanie użytkowników jest bezpłatne funkcji dla wszystkich użytkowników usługi MFA. Umożliwia toogive użytkowników hello opcji przebiegu tooby MFA przez liczbę dni, po wykonaniu pomyślne Zaloguj się przy użyciu usługi MFA. To zwiększają użyteczność, minimalizując hello ile razy użytkownik może wykonać weryfikacji dwuetapowej na powitania tego samego urządzenia.

Jednak w przypadku złamania zabezpieczeń konta lub urządzenia, zapamiętywanie uwierzytelniania Wieloskładnikowego na zaufanych urządzeniach może mieć wpływ na bezpieczeństwo. Jeśli zostanie naruszone bezpieczeństwo konta firmowego lub zaufanego urządzenia utraty lub kradzieży, [Przywróć uwierzytelnianie wieloskładnikowe na wszystkich urządzeniach](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Ta akcja odwołuje hello zaufanego stanu ze wszystkich urządzeń, a użytkownik hello jest wymagana tooperform ponownie weryfikacji dwuetapowej. Można także skonfigurować Twoje MFA toorestore użytkowników na ich własnych urządzeniach za pomocą instrukcji hello w [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Jak to działa

Pamiętaj o tym, usługa Multi-Factor Authentication działa przez ustawienie trwały plik cookie w przeglądarce hello, gdy użytkownik hello "nie pytaj ponownie o **X** dni" pole podczas logowania. Hello użytkownik nie będzie monitowany o MFA ponownie z tym broswer do momentu wygaśnięcia pliku cookie hello. Jeśli użytkownik hello otwiera innej przeglądarki na hello samego urządzenia lub czyści ich plików cookie, są one zostanie wyświetlony monit o tooverify ponownie. 

Witaj "nie pytaj ponownie o **X** dni" pole wyboru nie jest widoczne w aplikacjach korzystających z przeglądarki, czy obsługują one nowoczesnego uwierzytelniania. Te aplikacje używaj tokenów odświeżania, zapewniające nowe tokeny dostępu, co godzinę. Podczas sprawdzania poprawności tokenu odświeżania usługi Azure AD sprawdza, czy hello ostatniej weryfikacji dwuetapowej czasu został wykonane został hello skonfigurowane liczbę dni. 

W związku z tym zapamiętywanie uwierzytelniania Wieloskładnikowego na zaufanych urządzeniach zmniejsza liczbę hello uwierzytelnienia w usłudze aplikacje sieci web (które zwykle monit zawsze), ale zwiększa hello liczbę uwierzytelnień dla klientów uwierzytelniania nowoczesny, (które zwykle Monituj co 90 dni).

> [!NOTE]
>Ta funkcja nie jest zgodny z funkcją "Wylogowuj mnie" hello usług AD FS, gdy użytkownicy wykonują weryfikacji dwuetapowej dla usług AD FS za pomocą serwera usługi Azure MFA hello lub rozwiązanie MFA innych firm. Jeśli użytkownicy w usługach AD FS wybierz opcję "Wylogowuj mnie" i zaznaczyć swoje urządzenia jako zaufane dla usługi MFA, będą mogli tooverify po wygaśnięciu hello "Pamiętaj MFA" Liczba dni. Usługi Azure AD żądań weryfikacji dwuetapowej świeże, ale usług AD FS zwraca token z hello oryginalnego MFA oświadczeń i Data zamiast wykonywania ponownie weryfikacji dwuetapowej. To powoduje rozpoczęcie pętlę weryfikacji między Azure AD i usług AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Włączanie uwierzytelniania wieloskładnikowego Zapamiętaj
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź na stronie ustawień usługi MFA toohello zgodnie z instrukcjami hello na początku hello tego artykułu.
3. Na stronie ustawień usługi hello, w obszarze zarządzania ustawieniami urządzenia użytkownika, należy sprawdzić hello **użytkownicy tooremember uwierzytelniania wieloskładnikowego na zaufanych urządzeniach** pole.
   ![Należy pamiętać, urządzenia](./media/multi-factor-authentication-whats-next/remember.png)
4. Ustaw hello liczbę dni, które mają weryfikacji dwuetapowej toobypass tooallow hello zaufanych urządzeń. domyślne Hello jest 14 dni.
5. Kliknij pozycję **Zapisz**.
6. Kliknij przycisk **Zamknij**.

### <a name="mark-a-device-as-trusted"></a>Oznacz jako zaufanego urządzenia

Po włączeniu tej funkcji, użytkowników można oznaczyć jako zaufane, gdy urządzenie zalogują się sprawdzając **nie pytaj ponownie**.

![Nie pytaj ponownie — zrzut ekranu](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Metody wyboru weryfikacji
Można wybrać metody weryfikacji, które są dostępne dla użytkowników. Poniższa tabela Hello zawiera krótki przegląd każdej metody.

Gdy użytkownicy rejestrują swoje konta dla usługi MFA, decydują ich metodę weryfikacji preferowanego poza hello opcje, które są włączone. Witaj wskazówki dotyczące procesu rejestracji znajdują się w [Skonfiguruj moje konto na potrzeby weryfikacji dwuetapowej](multi-factor-authentication-end-user-first-time.md)

| Metoda | Opis |
|:--- |:--- |
| Wywołanie toophone |Umieszcza wykonywane automatyczne połączenie głosowe. Witaj Witaj odpowiedzi użytkownika Wywołaj i naciska klawisz # na powitania phone klawiatury tooauthenticate. Ten numer telefonu nie jest zsynchronizowane tooon lokalnej usługi Active Directory. |
| Tekst komunikatu toophone |Wysyła wiadomość tekstową zawierającą kod weryfikacyjny. Użytkownik Hello jest tooeither zostanie wyświetlony monit o odpowiedź toohello wiadomość SMS, wysyłając kod weryfikacyjny hello lub kod weryfikacyjny hello tooenter do hello w interfejsie logowania. |
| Powiadomienia za pomocą aplikacji mobilnej |Wysyła phone tooyour powiadomień wypychanych lub zarejestrowanym urządzeniu. Hello użytkownika widoków hello powiadomień i wybiera **Sprawdź** toocomplete weryfikacji. <br>Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Kod weryfikacyjny z aplikacji mobilnej |Aplikacja Microsoft Authenticator Hello generuje nowy kod OATH weryfikacji co 30 sekund. Użytkownik Hello wejścia ten kod weryfikacyjny hello w interfejsie logowania.<br>Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Jak tooenable/wyłączanie metody uwierzytelniania
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź na stronie ustawień usługi MFA toohello zgodnie z instrukcjami hello na początku hello tego artykułu.
3. Na stronie ustawień usługi hello w obszarze Opcje weryfikacji wybrać/anulować wybór opcji hello mają toouse.
   ![Opcje weryfikacji](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Kliknij pozycję **Zapisz**.
5. Kliknij przycisk **Zamknij**.

