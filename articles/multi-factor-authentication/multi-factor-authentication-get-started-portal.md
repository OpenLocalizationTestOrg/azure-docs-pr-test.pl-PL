---
title: "portal aaaUser dla serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest hello Azure Multi-Factor authentication strona opisujące, jak tooget wprowadzenie do usługi Azure MFA i hello portal użytkowników."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portal użytkowników na powitania serwera usługi Azure Multi-Factor Authentication

Hello portal użytkowników to witryna sieci web IIS, który umożliwia tooenroll użytkowników w usłudze Azure Multi-Factor Authentication (MFA) i obsługę kont. Użytkownik może zmienić swój numer telefonu, zmianę kodu PIN lub wybierz toobypass weryfikacji dwuetapowej podczas ich następnego logowania.

Użytkownicy Zaloguj się w portalu użytkowników toohello ich zwykłej nazwy użytkownika i hasło, następnie ukończenia wywołania weryfikacji dwuetapowej albo odpowiedzi toocomplete pytania zabezpieczeń uwierzytelniania. Jeśli rejestracja użytkowników jest dozwolona, użytkownicy skonfigurować ich numer telefonu i kod PIN hello zalogują się po raz pierwszy w portalu użytkowników toohello.

Portal użytkowników Administratorzy mogą skonfigurować i przyznane uprawnienia tooadd nowych użytkowników i Aktualizuj istniejących użytkowników.

W zależności od środowiska, może być toodeploy hello użytkownika portalu na powitania tego samego serwera jako serwera usługi Azure Multi-Factor Authentication lub na innym serwerze skierowane do Internetu.

![Portal użytkowników usługi MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portal użytkowników Hello jest dostępna tylko w aplikacji serwer Multi-Factor Authentication. Uwierzytelnianie wieloskładnikowe w chmurze hello, zapoznaj się z toohello użytkowników [konfiguracji konta na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-first-time.md) lub [zarządzać ustawieniami na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Instalowanie zestawu SDK usług sieci web hello

W każdym z tych scenariuszy, jeśli hello Azure Multi-Factor Authentication Web Service SDK jest **nie** już zainstalowane na powitania serwera usługi Azure Multi-Factor Authentication (MFA), pełny hello kroków poniżej.

1. Otwórz program hello aplikacji serwer Multi-Factor Authentication.
2. Przejdź toohello **zestawu SDK usług sieci Web** i wybierz **Zainstaluj usługę Web Service SDK**.
3. Zainstaluj pełną hello przy użyciu wartości domyślnych hello, chyba że potrzebne toochange ich jakiegoś powodu.
4. Powiązania witryny toohello certyfikatu SSL w usługach IIS.

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze IIS, zobacz artykuł hello [jak tooSet zabezpieczeń SSL w usługach IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Witaj zestawu SDK usług sieci Web musi być zabezpieczona za pomocą certyfikatu SSL. W tym celu wystarczy certyfikat z podpisem własnym. Zaimportuj certyfikat hello w magazynie "Zaufane główne urzędy certyfikacji" hello hello konta komputera lokalnego na serwerze sieci web portalu użytkowników hello, tak, aby podczas inicjowania połączenia SSL hello zaufany certyfikat.

![Ustawienia konfiguracji serwera usługi MFA — zestaw SDK usługi internetowej](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Wdrożenie aplikacji portal użytkowników hello na powitania tym samym serwerze co powitania serwera usługi Azure Multi-Factor Authentication

Witaj następujące wymagania wstępne są wymagane tooinstall hello użytkownika portalu na powitania **tym samym serwerze** jako hello Azure aplikacji serwer Multi-Factor Authentication:

* Usługi IIS, w tym usługi ASP.NET, i zgodność metabazy IIS 6 (dla usług IIS 7 lub nowszych)
* Konta z prawami administratora hello komputera i domeny, jeśli ma to zastosowanie. Konto Hello na potrzeby grupy zabezpieczeń usługi Active Directory toocreate uprawnienia.
* Zabezpiecz hello portal użytkowników za pomocą certyfikatu SSL.
* Zabezpiecz hello Azure Multi-Factor Authentication Web Service SDK za pomocą certyfikatu SSL.

toodeploy hello użytkownika portalu, wykonaj następujące kroki:

1. Otwórz konsolę serwera usługi Azure Multi-Factor Authentication hello, kliknij przycisk hello **Portal użytkowników** ikonę w hello pozostałych menu, kliknij przycisk **Zainstaluj Portal użytkowników**.
2. Zainstaluj pełną hello przy użyciu wartości domyślnych hello, chyba że potrzebne toochange ich jakiegoś powodu.
3. Powiązania witryny toohello certyfikatu SSL w usługach IIS

   > [!NOTE]
   > Ten certyfikat SSL jest przeważnie publicznie podpisanym certyfikatem SSL.

4. Otwórz przeglądarkę sieci web za pomocą dowolnego komputera i przejdź do adresu URL toohello zainstalowaną hello portalu użytkowników (przykład: https://mfa.contoso.com/MultiFactorAuth). Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.

![Instalacja portalu użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze IIS, zobacz artykuł hello [jak tooSet zabezpieczeń SSL w usługach IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Wdrożenie aplikacji portal użytkowników hello na osobnym serwerze

Jeśli serwera hello, w którym jest uruchomiona serwera usługi Azure Multi-Factor Authentication nie jest skierowane do Internetu, należy zainstalować portal użytkowników hello na **oddzielne, internetowy serwer**.

Jeśli Twoja organizacja korzysta z hello aplikacji Microsoft Authenticator jako jedną z metod weryfikacji hello i chcesz toodeploy portal użytkowników hello na osobnym serwerze, wykonaj hello następujące wymagania:

* Użyj wersji 6.0 lub nowszej powitania serwera usługi Azure Multi-Factor Authentication.
* Zainstaluj portal użytkowników hello na internetowy serwer sieci web, który jest uruchomiony program Microsoft internet Information Services (IIS) 6.x lub nowszego.
* Korzystając z usług IIS 6.x, upewnij się, programu ASP.NET v2.0.50727 jest zainstalowana, zarejestrowane i ustawiona zbyt**dozwolone**.
* W przypadku użycia usług IIS 7.x lub nowszych zachowanie zgodności usług IIS z uwzględnieniem uwierzytelniania podstawowego, z technologią ASP.NET i metabazą usług IIS 6.
* Zabezpiecz hello portal użytkowników za pomocą certyfikatu SSL.
* Zabezpiecz hello Azure Multi-Factor Authentication Web Service SDK za pomocą certyfikatu SSL.
* Upewnij się, że tego hello portalu użytkownika można łączyć toohello Azure Multi-Factor Authentication Web Service SDK za pośrednictwem protokołu SSL.
* Upewnij się, tego hello portalu użytkownika można uwierzytelniać toohello Azure Multi-Factor Authentication Web Service SDK w grupie zabezpieczeń "Administratorzy aplikacji PhoneFactor" hello przy użyciu hello poświadczenia konta usługi. Tego konta usługi i grupy muszą istnieć w usłudze Active Directory, jeśli na powitania serwera usługi Azure Multi-Factor Authentication działa na serwerze przyłączonym do domeny. Na powitania serwera usługi Azure Multi-Factor Authentication istnieje lokalnie tego konta usługi i grupy, ponieważ nie jest tooa przyłączone do domeny.

Instalowanie portalu użytkowników hello na serwerze innym niż powitania serwera usługi Azure Multi-Factor Authentication wymaga hello następujące kroki:

1. **Na powitania serwera usługi MFA**, przejdź do ścieżki instalacji toohello (przykład: C:\Program Files\Multi-Factor Authentication Server) i kopiowania pliku hello **MultiFactorAuthenticationUserPortalSetup64** tooa lokalizacji dostępne toohello internetowy serwer, którym zostanie on zainstalowany.
2. **Na serwerze sieci web internetowy hello**, uruchom plik instalacyjny hello MultiFactorAuthenticationUserPortalSetup64 jako administrator, zmień hello lokacji, w razie potrzeby i zmienić hello wirtualnej katalogu tooa krótką nazwę, jeśli chcesz.
3. Powiązania witryny toohello certyfikatu SSL w usługach IIS.

   > [!NOTE]
   > Ten certyfikat SSL jest przeważnie publicznie podpisanym certyfikatem SSL.

4. Przeglądaj zbyt**C:\inetpub\wwwroot\MultiFactorAuth**
5. Edytuj hello plik Web.Config w Notatniku

    * Znajdź klucz hello **"USE_WEB_SERVICE_SDK"** i zmienić **wartość = "false"** zbyt**wartość = "true"**
    * Znajdź klucz hello **"Wartość pozycji WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** i zmienić **wartość = ""** za**wartość = "Domena\użytkownik"** domena\nazwa użytkownika w przypadku konta usługi, który jest częścią Grupy "Administratorzy aplikacji PhoneFactor".
    * Znajdź klucz hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** i zmienić **wartość = ""** za**wartość = "Password"** gdzie hasło jest hasło hello hello usługi Wprowadzona w poprzednim wierszu hello konta.
    * Znajdź wartość hello **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** i zmienić toohello adres URL tego symbolu zastępczego URL zestawu SDK usługi sieci Web zainstalowano w kroku 2.
    * Zapisz plik Web.Config hello i zamknij Notatnik.

6. Otwórz przeglądarkę sieci web za pomocą dowolnego komputera i przejdź do adresu URL toohello zainstalowaną hello portalu użytkowników (przykład: https://mfa.contoso.com/MultiFactorAuth). Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze IIS, zobacz artykuł hello [jak tooSet zabezpieczeń SSL w usługach IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Skonfiguruj ustawienia portalu użytkowników w powitania serwera usługi Azure Multi-Factor Authentication

Po zainstalowaniu tego portalu użytkownika hello należy tooconfigure powitania serwera usługi Azure Multi-Factor Authentication toowork hello Portal.

1. W konsoli serwera usługi Azure Multi-Factor Authentication powitania kliknij hello **Portal użytkowników** ikony. Na karcie Ustawienia hello, wprowadź nazwę hello adresu URL toohello użytkownika portalu w hello **adres URL portalu użytkownika** pola tekstowego. Włączenie funkcji poczty e-mail tego adresu URL znajduje się w wiadomościach e-mail hello, które są wysyłane toousers importowane do powitania serwera usługi Azure Multi-Factor Authentication.
2. Wybierz ustawienia hello, które mają toouse w hello Portal użytkowników. Na przykład, jeśli użytkownicy mogą toochoose ich metod uwierzytelniania, upewnij się, że **użytkownicy metody tooselect** jest zaznaczone, oraz metody hello mogą wybrać z.
3. Zdefiniować, kto powinien być Administratorzy na powitania **Administratorzy** kartę. Można utworzyć szczegółowego uprawnienia administracyjne, przy użyciu pola wyboru hello i list rozwijanych w polach Dodaj/Edytuj hello.

Konfiguracja opcjonalna:
- **Pytania zabezpieczające** — Zdefiniuj pytania zabezpieczające dla Twojego środowiska i hello języka pojawią się one w zatwierdzeniu.
- **Przekazane sesje** — skonfiguruj integrację portalu użytkownika z opartą na formularzu witryną internetową przy użyciu usługi MFA.
- **Zaufanych adresów IP** — Zezwalaj użytkownikom tooskip MFA podczas uwierzytelniania z listy zaufanych adresów IP lub zakresu.

![Konfiguracja portalu użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Serwer systemu Azure Multi-Factor Authentication zapewnia kilka opcji hello portal użytkowników. Witaj Poniższa tabela zawiera listę tych opcji oraz wyjaśnienie one używane.

| Ustawienia portalu użytkowników | Opis |
|:--- |:--- |
| Adres URL portalu użytkowników | Wprowadź adres URL hello gdzie portalu hello jest obsługiwana. |
| Uwierzytelnianie podstawowe | Określ typ hello toouse uwierzytelniania podczas rejestrowania się w portalu toohello. Dostępne opcje to Windows, Radius lub LDAP. |
| Zezwalaj użytkownikom toolog w | Zezwalaj tooenter użytkowników na nazwy użytkownika i hasła na powitania strony logowania dla aplikacji portal użytkowników hello. Jeśli ta opcja nie jest zaznaczona, pola hello są wygaszone. |
| Zezwalaj na rejestrację użytkownika | Zezwalaj tooenroll użytkownika w usłudze Multi-Factor Authentication, wykonując ich ekran konfiguracji tooa monitujące o dodatkowe informacje, takie jak numer telefonu. Monit o zapasowy numer telefonu umożliwia użytkownikom toospecify numeru telefonu dodatkowej. Monituj o innych firm OATH token umożliwia toospecify użytkowników token OATH innej firmy. |
| Zezwalaj użytkownikom tooinitiate jednokrotnego obejścia | Zezwalaj użytkownikom tooinitiate jednorazowego obejścia. Jeśli użytkownik konfiguruje tę opcję, będzie trwało hello efekt następnym zalogowaniu użytkownika hello. Monituj o obejścia w sekundach zapewnia użytkownikowi hello z polem, dlatego mogą zmienić domyślną hello 300 sekund. W przeciwnym razie hello jednorazowe obejście dotyczy tylko 300 sekund. |
| Zezwalaj użytkownikom tooselect — metoda | Zezwalaj użytkownikom toospecify ich podstawowej metody kontaktu. Metodą tą może być połączenie telefoniczne, wiadomość SMS, aplikacja mobilna lub token OATH. |
| Zezwalaj użytkownikom tooselect języka | Zezwalaj użytkownikom toochange hello język, który jest używany dla hello rozmowy telefonicznej, wiadomości tekstowej, aplikacji mobilnej lub tokenu OATH. |
| Zezwalaj aplikacji mobilnej tooactivate użytkowników | Zezwalaj użytkownikom toogenerate aktywacji kod toocomplete hello aplikacji mobilnej proces aktywacji, który jest używany z serwerem hello.  Można również ustawić hello liczbę urządzeń, aktywować aplikacji hello, w zakresie od 1 do 10. |
| Użyj pytań zabezpieczających w przypadku uwierzytelniania rezerwowego | Umożliwia udzielenie odpowiedzi na pytania zabezpieczające w przypadku niepowodzenia weryfikacji dwuetapowej. Można określić hello liczbę pytań zabezpieczających, które pomyślnie odpowiedzi. |
| Zezwalaj na token OATH innej firmy tooassociate użytkowników | Zezwalaj użytkownikom toospecify token OATH innej firmy. |
| Użyj tokenu OATH w przypadku uwierzytelniania rezerwowego | Umożliwia użycie hello tokenu OATH w przypadku, gdy weryfikacja dwuetapowa zakończy się niepowodzeniem. Można również określić limit czasu sesji hello w minutach. |
| Włącz rejestrowanie | Włącz rejestrowanie na powitania portal użytkowników. Witaj pliki dziennika znajdują się w: C:\Program Files\Multi-Factor Authentication Server\Logs. |

Te ustawienia będą widoczne toohello użytkownika w portalu hello, gdy są włączone i są zarejestrowane w portalu użytkowników toohello.

![Ustawienia portalu użytkowników](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Samodzielna rejestracja użytkownika

Toosign Twojego użytkowników i rejestrowanie, należy wybrać hello **Zezwalaj toolog użytkowników w** i **Zezwalaj na rejestrację użytkowników** opcje na karcie Ustawienia hello. Należy pamiętać, że wybrane ustawienia hello wpływają na powitania użytkownika logowania.

Na przykład po zalogowaniu użytkownika w portalu użytkownika toohello powitania po raz pierwszy, następnie są one brane toohello ustawienia użytkownika uwierzytelnianie wieloskładnikowe Azure strony. W zależności od sposobu konfiguracji usługi Azure Multi-Factor Authentication, hello użytkownika może być możliwe tooselect ich metody uwierzytelniania.

Jeśli wybierz hello głosu wywołać metodę weryfikacji lub zostały wstępnie skonfigurowane toouse tej metody, strona hello monituje tooenter użytkownika hello ich głównego numeru telefonu i rozszerzenia, jeśli ma to zastosowanie. Może być również dozwolone tooenter zapasowy numer telefonu.

![Rejestrowanie podstawowych i zapasowych numerów telefonów](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Jeśli użytkownik hello jest wymagana toouse numeru PIN podczas uwierzytelniania, strony hello monituje o ich toocreate numeru PIN. Po wprowadzeniu swoje numery telefonów i numer PIN (jeśli dotyczy), hello użytkownik klika polecenie hello **Zadzwoń do mnie tooAuthenticate** przycisku. Usługa Azure Multi-Factor Authentication wykonuje połączeń telefonicznych weryfikacji toohello użytkownika głównego numeru telefonu. Użytkownik Hello musi odpowiedzieć hello połączeń telefonicznych i wprowadź swój kod PIN (jeśli dotyczy) i naciśnij klawisz # toomove na toohello następnego kroku procesu rejestracji samodzielnej hello.

Jeśli hello użytkownik wybiera metodę weryfikacji wiadomość hello lub zostało wstępnie skonfigurowane toouse tej metody, strony hello hello wyświetla użytkownikowi monit o ich numeru telefonu komórkowego. Jeśli hello użytkownika jest wymagane toouse numeru PIN podczas uwierzytelniania, strona hello także wyświetla monit o ich tooenter numeru PIN.  Po wprowadzeniu ich numer telefonu i numeru PIN (jeśli dotyczy), hello użytkownik klika polecenie hello **tekst mnie teraz tooAuthenticate** przycisku. Usługa Azure Multi-Factor Authentication wykonuje telefon komórkowy SMS weryfikacji toohello użytkownika. Witaj użytkownik otrzymuje hello wiadomość SMS z jednego-jednorazowej-kod dostępu (OTP), a następnie odpowiedzi toohello wiadomości z tego OTP oraz kod PIN (jeśli dotyczy).

![Wiadomość SMS z portalu użytkowników](./media/multi-factor-authentication-get-started-portal/text.png)

Jeśli hello użytkownik wybiera metodę weryfikacji hello aplikacji mobilnej, strona hello monituje hello aplikacji Microsoft Authenticator hello tooinstall użytkownika na urządzeniu i wygenerowanie kodu aktywacji. Po zainstalowaniu aplikacji hello, hello użytkownik kliknie przycisk Generuj kod aktywacji hello.

> [!NOTE]
> aplikacji Microsoft Authenticator hello toouse, hello użytkownika należy włączyć powiadomień wypychanych na swoim urządzeniu.

stronie powitania zostanie wyświetlony kod aktywacyjny i adres URL i obraz kodu kreskowego. Jeśli użytkownik hello jest wymagana toouse numeru PIN podczas uwierzytelniania, hello strony Ponadto monituje o ich tooenter numeru PIN. Użytkownik Hello wejścia hello kod aktywacji i adres URL w aplikacji Microsoft Authenticator hello lub używa hello kod kreskowy skanera tooscan hello kod kreskowy obrazu i kliknie przycisk Aktywuj hello.

Po ukończeniu aktywacji hello hello użytkownik klika polecenie hello **Uwierzytelnij mnie teraz** przycisku. Usługa Azure Multi-Factor Authentication wykonuje aplikacji mobilnej użytkownika toohello weryfikacji. Hello użytkownik musi wprowadzić kod PIN (jeśli dotyczy) i naciśnij przycisk Uwierzytelnij hello w ich toomove aplikacji mobilnej na toohello następnego kroku procesu rejestracji samodzielnej hello.

Jeśli administratorzy hello skonfigurowano powitania serwera usługi Azure Multi-Factor Authentication toocollect zabezpieczeń pytania i odpowiedzi, użytkownik hello następnie jest pobierany toohello pytania zabezpieczające strony. Witaj użytkownika należy wybrać cztery pytania zabezpieczające i podać odpowiedzi na pytania tootheir wybrane.

![Pytania zabezpieczające portalu użytkowników](./media/multi-factor-authentication-get-started-portal/secq.png)

Samodzielna rejestracja przez użytkownika Hello jest teraz ukończona i hello użytkownik jest zalogowany toohello portal użytkowników. Użytkownicy mogą zalogują się ponownie toohello portal użytkowników w dowolnym momencie w przyszłości toochange hello numery telefonów, numery PIN, metody uwierzytelniania i pytania zabezpieczające Jeśli zmiana ich metod jest dozwolona przez administratorów.

## <a name="next-steps"></a>Następne kroki

- [Wdrażanie hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md)
