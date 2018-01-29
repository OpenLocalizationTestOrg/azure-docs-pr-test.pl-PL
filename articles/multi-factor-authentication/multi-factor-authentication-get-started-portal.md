---
title: "Portal użytkowników serwera usługi Azure MFA | Microsoft Docs"
description: "Ta strona dotycząca usługi Azure Multi-Factor Authentication zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA i portalu użytkowników."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: 15f4ef7b70027a820dc50a9399891bbab77d7e12
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="user-portal-for-the-azure-multi-factor-authentication-server"></a>Portal użytkowników serwera usługi Azure Multi-Factor Authentication

Portal użytkowników to witryna internetowa usług IIS, dzięki której użytkownicy mogą zarejestrować się w usłudze Azure Multi-Factor Authentication (MFA) i obsługiwać swoje konta. Użytkownik może zmienić swój numer telefonu i numer PIN lub zdecydować o pominięciu weryfikacji dwuetapowej podczas następnego logowania.

Użytkownik loguje się do portalu użytkowników przy użyciu swojej zwykłej nazwy użytkownika oraz hasła, a następnie wykonuje połączenie uwierzytelniające weryfikacji dwuetapowej lub udziela odpowiedzi na pytanie zabezpieczające, aby ukończyć proces uwierzytelniania. Jeśli rejestracja użytkowników jest dozwolona, użytkownik może skonfigurować swój numer telefonu i numer PIN podczas pierwszego logowania do portalu użytkowników.

Można skonfigurować administratorów portalu użytkowników oraz przyznać im uprawnienia pozwalające dodawać nowych użytkowników i aktualizować istniejących.

W zależności od środowiska można wdrożyć portal użytkowników na tym samym serwerze co serwer usługi Azure Multi-Factor Authentication lub na innym serwerze internetowym.

![Portal użytkowników usługi MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> Portal użytkowników jest dostępny tylko na serwerze usługi Azure Multi-Factor Authentication. Jeśli korzystasz z usługi Multi-Factor Authentication w chmurze, przekieruj użytkowników do artykułu [Konfigurowanie konta na potrzeby weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-first-time.md) lub [Zarządzanie ustawieniami weryfikacji dwuetapowej](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-the-web-service-sdk"></a>Instalowanie zestawu SDK usługi sieci Web

W dowolnym scenariuszu, jeśli zestaw SDK usługi internetowej Azure Multi-Factor Authentication **nie** został jeszcze zainstalowany na serwerze usługi Azure Multi-Factor Authentication (MFA), wykonaj poniższe kroki.

1. Otwórz konsolę serwera usługi Multi-Factor Authentication.
2. Przejdź do **zestawu SDK usługi internetowej** i wybierz pozycję **Zainstaluj zestaw SDK usługi internetowej**.
3. Ukończ instalację przy użyciu ustawień domyślnych, o ile nie trzeba ich zmienić z dowolnej przyczyny.
4. Powiąż certyfikat SSL z witryną w usługach IIS.

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze usług IIS, zobacz artykuł [How to Set Up SSL on IIS (Jak skonfigurować protokół SSL w usługach IIS)](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Zestaw SDK usługi sieci Web musi zostać zabezpieczony za pomocą certyfikatu SSL. W tym celu wystarczy certyfikat z podpisem własnym. Zaimportuj certyfikat do magazynu „Zaufane główne urzędy certyfikacji” konta komputera lokalnego na serwerze internetowym portalu użytkowników, dzięki czemu magazyn uzna ten certyfikat za zaufany podczas inicjowania połączenia SSL.

![Ustawienia konfiguracji serwera usługi MFA — zestaw SDK usługi internetowej](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-the-user-portal-on-the-same-server-as-the-azure-multi-factor-authentication-server"></a>Wdrażanie portalu użytkowników na tym samym serwerze, na którym działa serwer usługi Azure Multi-Factor Authentication

W celu zainstalowania portalu użytkowników na **tym samym serwerze**, na którym działa serwer usługi Azure Multi-Factor Authentication, wymagane jest spełnienie następujących wymagań wstępnych:

* Usługi IIS, w tym usługi ASP.NET, i zgodność metabazy IIS 6 (dla usług IIS 7 lub nowszych)
* Konto z prawami administratora na danym komputerze i w danej domenie (jeśli ma zastosowanie). Konto wymaga uprawnień do tworzenia grup zabezpieczeń usługi Active Directory.
* Zabezpieczenie portalu użytkowników za pomocą certyfikatu SSL.
* Zabezpieczenie zestawu SDK usługi sieci Web usługi Azure Multi-Factor Authentication za pomocą certyfikatu SSL.

Aby wdrożyć portal użytkowników, wykonaj następujące czynności:

1. Otwórz konsolę usługi Azure Multi-Factor Authentication, kliknij ikonę **Portal użytkowników** w menu po lewej stronie i kliknij pozycję **Zainstaluj portal użytkowników**.
2. Ukończ instalację przy użyciu ustawień domyślnych, o ile nie trzeba ich zmienić z dowolnej przyczyny.
3. Tworzenie powiązania certyfikatu SSL z witryną w usługach IIS

   > [!NOTE]
   > Ten certyfikat SSL jest przeważnie publicznie podpisanym certyfikatem SSL.

4. Otwórz przeglądarkę internetową z dowolnego komputera i przejdź do adresu URL, pod którym zainstalowano portal użytkowników (np. https://mfa.contoso.com/MultiFactorAuth). Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.

![Instalacja portalu użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze usług IIS, zobacz artykuł [How to Set Up SSL on IIS (Jak skonfigurować protokół SSL w usługach IIS)](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-the-user-portal-on-a-separate-server"></a>Wdrażanie portalu użytkowników na osobnym serwerze

Jeśli serwer, na którym jest uruchomiony serwer usługi Azure Multi-Factor Authentication, nie jest dostępny z Internetu, należy zainstalować portal użytkowników na **osobnym serwerze dostępnym z Internetu**.

Jeśli organizacja używa aplikacji Microsoft Authenticator jako jednej z metod weryfikacji i chce wdrożyć portal użytkowników na własnym serwerze, upewnij się, że spełniono następujące wymagania:

* Używanie serwera usługi Multi-Factor Authentication w wersji 6.0 lub nowszej.
* Zainstalowanie portalu użytkowników na dostępnym z Internetu serwerze sieci Web z uruchomionymi usługami Microsoft Internet Information Services (IIS) w wersji 6.x lub nowszej.
* W przypadku użycia wersji IIS 6.x upewnij się, że program ASP.NET w wersji 2.0.50727 jest zainstalowany i zarejestrowany oraz że wybrano dla niego opcję **Dozwolone**.
* W przypadku użycia usług IIS 7.x lub nowszych zachowanie zgodności usług IIS z uwzględnieniem uwierzytelniania podstawowego, z technologią ASP.NET i metabazą usług IIS 6.
* Zabezpieczenie portalu użytkowników za pomocą certyfikatu SSL.
* Zabezpieczenie zestawu SDK usługi sieci Web usługi Azure Multi-Factor Authentication za pomocą certyfikatu SSL.
* Portal użytkowników musi być w stanie nawiązać połączenie z zestawem SDK usługi sieci Web usługi Azure Multi-Factor Authentication za pośrednictwem protokołu SSL.
* Portal użytkowników musi mieć możliwość uwierzytelnienia w zestawie SDK usługi sieci Web usługi Azure Multi-Factor Authentication przy użyciu poświadczeń konta usługi w grupie zabezpieczeń o nazwie „PhoneFactor Admins”. To konto usługi i ta grupa powinny istnieć w usłudze Active Directory, jeśli serwer usługi Azure Multi-Factor Authentication jest uruchomiony na serwerze przyłączonym do domeny. To konto usługi i ta grupa istnieją lokalnie na serwerze usługi Azure Multi-Factor Authentication, jeśli nie jest on przyłączony do domeny.

Zainstalowanie portalu użytkowników na serwerze innym niż serwer usługi Azure Multi-Factor Authentication wymaga wykonania następujących kroków:

1. **Na serwerze usługi MFA** przejdź do ścieżki instalacji (przykład: C:\Program Files\Multi-Factor Authentication Server), a następnie skopiuj plik **MultiFactorAuthenticationUserPortalSetup64** do lokalizacji dostępnej dla serwera z dostępem do Internetu, na którym zostanie on zainstalowany.
2. **Na internetowym serwerze dostępnym z Internetu** uruchom plik instalacji MultiFactorAuthenticationUserPortalSetup64 jako administrator, w miarę potrzeb zmieniając miejsce instalacji, a następnie, jeśli chcesz, zmień nazwę katalogu wirtualnego na krótką.
3. Powiąż certyfikat SSL z witryną w usługach IIS.

   > [!NOTE]
   > Ten certyfikat SSL jest przeważnie publicznie podpisanym certyfikatem SSL.

4. Przejdź do folderu **C:\inetpub\wwwroot\MultiFactorAuth**
5. Edytowanie pliku Web.Config w Notatniku

    * Znajdź klucz **"USE_WEB_SERVICE_SDK"** i zmień wartość **value="false"** na **value="true"**
    * Znajdź klucz **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** i zmień wartość **value=""** na **value="DOMAIN\User"**, gdzie DOMAIN\User to konto usługi będące częścią grupy „PhoneFactor Admins”.
    * Znajdź klucz **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** i zmień wartość **value=""** na **value="Password"**, gdzie Password to hasło konta usługi wprowadzonego w poprzednim wierszu.
    * Znajdź wartość **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** i zmień adres URL tego symbolu zastępczego na adres URL zestawu SDK usługi internetowej zainstalowanej w kroku 2.
    * Zapisz plik Web.Config i zamknij Notatnik.

6. Otwórz przeglądarkę internetową z dowolnego komputera i przejdź do adresu URL, pod którym zainstalowano portal użytkowników (np. https://mfa.contoso.com/MultiFactorAuth). Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze usług IIS, zobacz artykuł [How to Set Up SSL on IIS (Jak skonfigurować protokół SSL w usługach IIS)](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-the-azure-multi-factor-authentication-server"></a>Konfigurowanie ustawień portalu użytkowników na serwerze usługi Azure Multi-Factor Authentication

Po zainstalowaniu portalu użytkowników należy skonfigurować serwer usługi Azure Multi-Factor Authentication do pracy z portalem.

1. W konsoli serwera usługi Azure Multi-Factor Authentication kliknij ikonę **Portal użytkowników**. Na karcie Ustawienia wprowadź adres URL portalu użytkowników w polu tekstowym **Adres URL portalu użytkowników**. Jeśli włączono funkcję e-mail, podany adres URL zostanie uwzględniony w wiadomości e-mail wysyłanej do użytkowników po ich zaimportowaniu na serwer usługi Azure Multi-Factor Authentication.
2. Wybierz ustawienia, których chcesz użyć w portalu użytkowników. Jeśli na przykład użytkownicy mogą wybierać swoje metody uwierzytelniania, upewnij się, że jest zaznaczona opcja **Zezwalaj użytkownikom na wybór metody** oraz poszczególne metody uwierzytelniania, spośród których mogą wybierać użytkownicy.
3. Zdefiniuj, którzy użytkownicy powinni być administratorami, na karcie **Administratorzy**. Możesz utworzyć szczegółowe uprawnienia administracyjne, korzystając z pól wyboru i list rozwijanych w polach Dodaj/Edytuj.

Konfiguracja opcjonalna:
- **Pytania zabezpieczające** — zdefiniuj zatwierdzone pytania zabezpieczające dla środowiska oraz język, w którym mają być wyświetlane.
- **Przekazane sesje** — skonfiguruj integrację portalu użytkownika z opartą na formularzu witryną internetową przy użyciu usługi MFA.
- **Zaufane adresy IP** — zezwól użytkownikom na pomijanie usługi MFA podczas uwierzytelniania na podstawie listy zaufanych zakresów lub adresów IP.

![Konfiguracja portalu użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Serwer usługi Azure Multi-Factor Authentication zapewnia kilka opcji związanych z portalem użytkowników. Poniższa tabela zawiera listę tych opcji wraz z opisem ich zastosowania.

| Ustawienia portalu użytkowników | Opis |
|:--- |:--- |
| Adres URL portalu użytkowników | Umożliwia wprowadzenie adresu URL, pod którym jest hostowany portal. |
| Uwierzytelnianie podstawowe | Umożliwia określenie typu uwierzytelniania stosowanego podczas logowania się do portalu. Dostępne opcje to Windows, Radius lub LDAP. |
| Zezwalaj użytkownikom na logowanie | Umożliwia użytkownikom wprowadzenie swoich nazw i haseł na stronie logowania w portalu użytkowników. Jeśli ta opcja nie zostanie zaznaczona, pola są wyszarzone. |
| Zezwalaj na rejestrację użytkownika | Umożliwia użytkownikowi rejestrację w usłudze Multi-Factor Authentication, wyświetlając ekran konfiguracji z monitami o dodatkowe informacje, takie jak numer telefonu. Wybór opcji Monituj o zapasowy numer telefonu pozwala użytkownikom wprowadzić dodatkowy numer telefonu. Wybór opcji Monituj o token OATH innej firmy umożliwia użytkownikom podanie tokenu OATH innej firmy. |
| Zezwalaj użytkownikom na inicjowanie jednokrotnego obejścia | Umożliwia użytkownikom inicjowanie jednokrotnego obejścia. Jeśli użytkownik skonfiguruje tę opcję, zostanie ona zastosowana podczas następnego logowania użytkownika. Opcja Monituj o obejście (w sekundach) zapewnia użytkownikowi dostęp do pola opcji i pozwala zmienić wartość domyślną, jaką jest 300 sekund. Jeśli ta opcja nie zostanie wybrana, jednorazowe obejście będzie działać tylko przez 300 sekund. |
| Zezwalaj użytkownikom na wybór metody | Umożliwia użytkownikom wskazanie głównego sposobu kontaktu. Metodą tą może być połączenie telefoniczne, wiadomość SMS, aplikacja mobilna lub token OATH. |
| Zezwalaj użytkownikom na wybór języka | Umożliwia użytkownikom zmianę języka używanego w przypadku rozmów telefonicznych, wiadomości SMS, aplikacji mobilnej lub tokenów OATH. |
| Zezwalaj użytkownikom na uaktywnienie aplikacji mobilnej | Opcja umożliwia użytkownikom wygenerowanie kodu aktywacji w celu ukończenia procesu aktywacji aplikacji mobilnej, która jest używana w połączeniu z serwerem.  Można również ustawić liczbę urządzeń (od 1 do 10), na których użytkownik może dokonać aktywacji aplikacji. |
| Użyj pytań zabezpieczających w przypadku uwierzytelniania rezerwowego | Umożliwia udzielenie odpowiedzi na pytania zabezpieczające w przypadku niepowodzenia weryfikacji dwuetapowej. Można określić liczbę pytań zabezpieczających, na które należy udzielić poprawnej odpowiedzi. |
| Zezwalaj użytkownikom na skojarzenie tokenu OATH innej firmy | Pozwala użytkownikom na określenie tokenu OATH innej firmy. |
| Użyj tokenu OATH w przypadku uwierzytelniania rezerwowego | Umożliwia korzystanie z tokenów OATH w przypadku niepowodzenia weryfikacji dwuetapowej. Można również określić limit czasu sesji w minutach. |
| Włącz rejestrowanie | Włącza funkcję rejestrowania w portalu użytkowników. Pliki dziennika znajdują się w folderze: C:\Program Files\Multi-Factor Authentication Server\Logs. |

Te ustawienia stają się widoczne dla użytkownika w portalu po ich włączeniu oraz po zalogowaniu się do tego portalu.

![Ustawienia portalu użytkowników](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Samodzielna rejestracja użytkownika

Jeśli chcesz, aby użytkownicy mogli się logować i rejestrować, musisz wybrać opcje **Zezwalaj użytkownikom na logowanie** i **Zezwalaj na rejestrację użytkownika** w obszarze karty Ustawienia. Pamiętaj, że wybrane ustawienia wpływają na środowisko logowania użytkowników.

Na przykład użytkownik logujący się do portalu po raz pierwszy zostanie przeniesiony na stronę konfiguracji użytkownika usługi Azure Multi-Factor Authentication. W zależności od konfiguracji usługi Azure Multi-Factor Authentication użytkownik może być w stanie wybrać metodę uwierzytelniania.

Jeśli wybierze on metodę weryfikacji Połączenie głosowe lub jeśli usługa została wstępnie skonfigurowana pod kątem użycia tej metody, strona wyświetla monit o podanie podstawowego numeru telefonu użytkownika oraz, w razie potrzeby, numeru wewnętrznego. Użytkownik może także mieć możliwość wprowadzenia zapasowego numeru telefonu.

![Rejestrowanie podstawowych i zapasowych numerów telefonów](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Jeśli podczas uwierzytelniania wymagane jest wprowadzenie przez użytkownika numeru PIN, na stronie wyświetla się także monit o utworzenie numeru PIN. Po wprowadzeniu numerów telefonów i numeru PIN (jeśli dotyczy) użytkownik klika przycisk **Połącz się teraz ze mną w celu uwierzytelnienia**. Usługa Azure Multi-Factor Authentication przeprowadza weryfikację w drodze połączenia telefonicznego z podstawowym numerem telefonu użytkownika. Użytkownik musi odebrać połączenie i wprowadzić numer PIN (jeśli ma zastosowanie), a następnie nacisnąć klawisz #, aby przejść do następnego kroku procesu samodzielnej rejestracji.

Jeśli użytkownik wybierze metodę weryfikacji Wiadomość SMS lub jeśli wstępna konfiguracja zakłada użycie tej metody, na stronie jest wyświetlany monit o wprowadzenie numeru telefonu komórkowego. Jeśli podczas uwierzytelniania wymagane jest wprowadzenie przez użytkownika numeru PIN, na stronie wyświetla się także monit o wprowadzenie numeru PIN.  Po wprowadzeniu numeru telefonu i numeru PIN (jeśli dotyczy) użytkownik klika przycisk **Wyślij teraz do mnie wiadomość SMS w celu uwierzytelnienia**. Usługa Azure Multi-Factor Authentication przeprowadza weryfikację SMS z użyciem telefonu komórkowego użytkownika. Użytkownik otrzymuje wiadomość SMS z jednorazowym kodem dostępu, a następnie w odpowiedzi na wiadomość podaje ten kod oraz numer PIN (jeśli dotyczy).

![Wiadomość SMS z portalu użytkowników](./media/multi-factor-authentication-get-started-portal/text.png)

Jeśli użytkownik wybierze metodę weryfikacji z użyciem aplikacji mobilnej, na stronie jest wyświetlany monit o zainstalowanie aplikacji Microsoft Authenticator na urządzeniu i wygenerowanie kodu aktywacji. Po zainstalowaniu aplikacji użytkownik klika przycisk Generuj kod aktywacji.

> [!NOTE]
> Aby móc używać aplikacji Microsoft Authenticator, użytkownik musi włączyć powiadomienia wypychane dla swojego urządzenia.

Na stronie zostanie wyświetlony kod aktywacji oraz adres URL wraz z obrazem kodu kreskowego. Jeśli podczas uwierzytelniania wymagane jest wprowadzenie przez użytkownika numeru PIN, na stronie wyświetla się dodatkowo monit o wprowadzenie numeru PIN. Użytkownik wprowadza kod aktywacji i adres URL w aplikacji Microsoft Authenticator lub korzysta ze skanera kodów kreskowych w celu zeskanowania obrazu kodu kreskowego, a następnie klika przycisk Aktywuj.

Po zakończeniu aktywacji użytkownik klika przycisk **Uwierzytelnij mnie teraz**. Usługa Azure Multi-Factor Authentication przeprowadza weryfikację z użyciem aplikacji mobilnej używanej przez użytkownika. Użytkownik musi wprowadzić numer PIN (jeśli ma zastosowanie), a następnie nacisnąć przycisk Uwierzytelnij w aplikacji mobilnej, aby przejść do następnego kroku procesu samodzielnej rejestracji.

Jeśli administrator skonfigurował serwer usługi Azure Multi-Factor Authentication pod kątem gromadzenia pytań zabezpieczających oraz odpowiedzi na nie, użytkownik zostaje następnie przeniesiony na stronę pytań zabezpieczających. Użytkownik musi wybrać cztery pytania zabezpieczające i podać odpowiedzi na nie.

![Pytania zabezpieczające portalu użytkowników](./media/multi-factor-authentication-get-started-portal/secq.png)

Proces samodzielnej rejestracji użytkownika zostaje zakończony, a użytkownik zostaje zalogowany do portalu użytkowników. Jeśli administratorzy zapewnią możliwość zmiany wybranej metody, użytkownicy mogą w dowolnym momencie ponownie zalogować się do portalu użytkowników, aby zmienić numery telefonów, numer PIN, metody uwierzytelniania oraz pytania zabezpieczające.

## <a name="next-steps"></a>Następne kroki

- [Wdrażanie usługi internetowej aplikacji mobilnej serwera Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server-webservice.md)