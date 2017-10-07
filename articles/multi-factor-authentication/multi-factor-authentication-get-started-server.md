---
title: "aaaGetting uruchomić serwera usługi Azure Multi-Factor Authentication | Dokumentacja firmy Microsoft"
description: "Jest to hello Azure Multi-Factor authentication strony, opisujące, jak tooget pracę z serwera usługi Azure MFA."
services: multi-factor-authentication
keywords: serwer uwierzytelniania, strona aktywacji aplikacji azure multi factor authentication, pobieranie serwera uwierzytelniania
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Wprowadzenie do powitania serwera usługi Azure Multi-Factor Authentication

<center>![Lokalna usługa MFA](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Teraz, Ustaliliśmy toouse lokalnej aplikacji serwer Multi-Factor Authentication, możemy rozpocząć pracę. Ta strona obejmuje instalację nowej powitania serwera i konfigurowanie go przy użyciu lokalnej usługi Active Directory. Jeśli już zainstalowany serwer usługi MFA hello i szukasz tooupgrade, zobacz [uaktualnienia toohello najnowsze serwera usługi Azure Multi-Factor Authentication](multi-factor-authentication-server-upgrade.md). Jeśli szukasz informacji na temat instalowania tylko hello usługi sieci web, zobacz [wdrażanie hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planowanie wdrożenia

Przed pobraniem powitania serwera usługi Azure Multi-Factor Authentication zastanowić, jakie są wymagania dotyczące wysokiej dostępności i obciążenia, na których. Użyj tego toodecide informacje, jak i gdzie toodeploy.

Dobrą praktyką hello liczbę użytkowników jest hello ilość pamięci, należy oczekiwać tooauthenticate na bieżąco.

| Użytkownicy | Pamięć RAM |
| ----- | --- |
| 1–10 000 | 4 GB |
| 10 001–50 000 | 8 GB |
| 50 001–100 000 | 12 GB |
| 100 000–200 001 | 16 GB |
| 200 001+ | 32 GB |

Czy potrzebna tooset wielu serwery wysokiej dostępności lub równoważenia obciążenia? Istnieje wiele sposobów tooset tej konfiguracji z serwera usługi Azure MFA. Po zainstalowaniu pierwszego serwera usługi MFA Azure staje się hello wzorca. Wszelkie dodatkowe serwery stają się podrzędnego i automatyczną synchronizację z głównego hello użytkowników i konfiguracji. Następnie można skonfigurować jeden serwer podstawowy i rest hello działają zgodnie z kopii zapasowej, lub skonfigurować równoważenia wszystkim serwerom hello obciążenia.

Główny serwera usługi Azure MFA przejdzie do trybu offline, serwerów podrzędnych hello można nadal przetwarzają żądania weryfikacji dwuetapowej. Jednak nie można dodać nowych i istniejących użytkowników nie można zaktualizować ustawień, dopóki wzorzec hello jest znowu w trybie online lub podrzędnym pobiera podwyższenia poziomu.

### <a name="prepare-your-environment"></a>Przygotowywanie środowiska

Upewnij się, że serwer hello, używanego dla usługi Azure Multi-Factor Authentication spełnia hello następujące wymagania:

| Wymagania serwera Azure Multi-Factor Authentication | Opis |
|:--- |:--- |
| Sprzęt |<li>200 MB wolnego miejsca na dysku twardym</li><li>Procesor umożliwiający obsługę architektury x32 lub x64</li><li>Co najmniej 1 GB pamięci RAM</li> |
| Oprogramowanie |<li>Windows Server 2008 lub nowszy, jeśli hello host jest system operacyjny serwera</li><li>Windows 7 lub nowszy, jeśli hello host jest system operacyjny klienta</li><li>Oprogramowanie Microsoft .NET 4.0 Framework</li><li>Usługi IIS 7.0 lub nowszy, jeśli instalowanie hello użytkownika portalu sieci web usługi lub zestawu SDK</li> |

### <a name="azure-mfa-server-components"></a>Składniki serwera usługi Azure MFA

W skład serwera usługi Azure MFA wchodzą trzy składniki internetowe:

* Usługa SDK — umożliwia komunikację z hello inne składniki i jest zainstalowany na serwerze aplikacji usługi Azure MFA hello sieci Web
* Portal użytkowników — witryny sieci web usług IIS, który umożliwia tooenroll użytkowników w usłudze Azure Multi-Factor Authentication (MFA) i obsługę kont.
* Usługi sieci Web aplikacji mobilnej — umożliwia przy użyciu aplikacji mobilnej, takie jak aplikacja Microsoft Authenticator hello na potrzeby weryfikacji dwuetapowej.

Wszystkie trzy składniki można zainstalować na powitania tym samym serwerze, jeśli serwer hello jest połączonych z Internetem. Jeśli podzielenie hello składników, hello zestawu SDK usług sieci Web jest zainstalowana na serwerze aplikacji hello Azure MFA i hello użytkownika portalu i usługi sieci Web aplikacji mobilnej są zainstalowane na serwerze skierowane do Internetu.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Wymagania serwera Azure Multi-Factor Authentication dotyczące zapory

Każdy serwer usługi MFA musi być możliwe toocommunicate na toohello wychodzącego z portu 443 następujące adresy:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Jeśli wychodzącego zapory są ograniczone na porcie 443, otwórz hello następujące zakresy adresów IP:

| Podsieć IP | Maska sieci | Zakres adresów IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Jeśli nie używasz funkcji potwierdzania zdarzeń hello, a użytkownicy nie są używane tooverify aplikacji mobilnych z urządzeń w sieci firmowej hello, wystarczy hello następujących zakresów:

| Podsieć IP | Maska sieci | Zakres adresów IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Pobierz powitania serwera usługi Azure Multi-Factor Authentication

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**
3. Kliknij pozycję **Użytkownicy i grupy**
4. Kliknij pozycję **Wszyscy użytkownicy**
5. Kliknij pozycję **Multi-Factor Authentication**
6. W obszarze **uwierzytelniania wieloskładnikowego** wybierz pozycję **ustawienia usługi**

   ![Strona Ustawienia usługi](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Na stronie ustawień usługi hello u dołu ekranu hello powitania kliknij **Przejdź toohello portal**. Zostanie otwarta nowa strona.
7. Kliknij pozycję **Pliki do pobrania**.
8. Kliknij przycisk hello **Pobierz** link i Zapisz hello Instalatora.

   ![Pobieranie serwera usługi MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Nie zamykaj tej strony jako tooit odnoszą się po uruchomiony Instalator hello.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Instalowanie i konfigurowanie powitania serwera usługi Azure Multi-Factor Authentication

Teraz, po jej pobraniu powitania serwera należy zainstalować i skonfigurować je. Upewnij się, że ten serwer hello, którą instalujesz na spełnia wymagania wymienione w sekcji planowania hello.

1. Kliknij dwukrotnie hello pliku wykonywalnego.
2. Na ekranie powitania wybierz Folder instalacji upewnij się, wybrany folder hello jest poprawna, a następnie kliknij przycisk **dalej**.
3. Po zakończeniu instalacji powitania kliknij **Zakończ**.  Uruchamia Kreatora konfiguracji Hello.
4. W konfiguracji hello kreatora ekran powitalny, sprawdź **Pomiń przy użyciu hello Kreator konfiguracji uwierzytelniania** i kliknij przycisk **dalej**.  Kreator Hello zamyka i hello uruchamiania serwera.

   ![Chmura](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Wróć na stronie powitania, który został pobrany serwer hello z kliknij hello **Generuj poświadczenia aktywacji** przycisku. Skopiuj te informacje do powitania serwera usługi Azure MFA w polach hello, pod warunkiem, a następnie kliknij przycisk **Aktywuj**.

## <a name="send-users-an-email"></a>Wysyłanie wiadomości e-mail do użytkowników

Wdrażanie tooease, Zezwalaj toocommunicate serwera usługi MFA z użytkownikami. Serwera usługi MFA można wysłać wiadomości e-mail tooinform ich, że zostały one zarejestrowane na potrzeby weryfikacji dwuetapowej.

Witaj poczty e-mail, możesz wysłać powinna zostać określona przez sposób konfigurowania użytkowników na potrzeby weryfikacji dwuetapowej. Na przykład jeśli numery telefonów mogą tooimport z katalogu firmy hello, powitalne wiadomości e-mail powinny zawierać hello domyślnych numerów telefonów, tak, aby użytkownicy wiedzieli, jakie tooexpect. Nie należy importować numery telefonów, czy użytkownicy będą aplikacji mobilnej hello toouse, wysyłania ich wiadomości e-mail, który kieruje toocomplete ich rejestracji konta. Dołącz toohello hyperlink portalu użytkownika usługi Azure Multi-Factor Authentication hello poczty e-mail.

Hello zawartości wiadomości e-mail hello zmienia się również w zależności od metody hello weryfikacji ustawioną dla użytkownika hello (połączenie telefoniczne, SMS lub aplikacja mobilna).  Na przykład jeśli użytkownik hello jest wymagane toouse numeru PIN podczas uwierzytelniania, powitalne wiadomości e-mail dowie się, co ich początkowego kodu PIN została ustawiona jako.  Użytkownicy są wymagane toochange swój kod PIN podczas ich pierwszym weryfikacji.

### <a name="configure-email-and-email-templates"></a>Konfigurowanie wiadomości e-mail i szablonów wiadomości e-mail

Kliknij ikonę e-mail hello na powitania po lewej stronie tooset hello ustawień do wysyłania tych wiadomości e-mail. Ta strona jest, gdzie można wprowadzić informacje hello SMTP poczty e-mail serwera i wysyłania sprawdzając hello **wysyłania wiadomości e-mail toousers** pole wyboru.

![Konfiguracja poczty e-mail serwera usługi MFA](./media/multi-factor-authentication-get-started-server/email1.png)

Na karcie treść wiadomości E-mail hello można wyświetlić hello szablonów wiadomości e-mail, które są dostępne toochoose z. W zależności od sposobu konfiguracji weryfikację dwuetapową tooperform użytkowników wybierz hello szablon, który najlepiej odpowiada użytkownik.

![Szablony poczty e-mail serwera usługi MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importowanie użytkowników z usługi Active Directory

Obecnie jest zainstalowany ten serwer hello ma tooadd użytkowników. Możesz wybrać toocreate je ręcznie, importowanie użytkowników z usługi Active Directory, lub skonfigurować automatyczne synchronizacji z usługą Active Directory.

### <a name="manual-import-from-active-directory"></a>Ręczne importowanie z usługi Active Directory

1. Powitania serwera usługi Azure MFA, powitania po lewej stronie, wybierz **użytkowników**.
2. U dołu hello, zaznacz pole wyboru **importowania z usługi Active Directory**.
3. Teraz możesz albo wyszukać dla poszczególnych użytkowników lub hello wyszukiwania AD directory jednostki organizacyjne z użytkownikami w nich.  W takim przypadku określono hello użytkowników w jednostce Organizacyjnej.
4. Zaznacz wszystkich użytkowników hello na powitania prawo i kliknij **importu**.  Zostanie wyświetlone okno podręczne informujące, że proces został zakończony pomyślnie.  Witaj Zamknij okno importu.

   ![Importowanie użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Automatyczna synchronizacja z usługą Active Directory

1. Powitania serwera usługi Azure MFA, powitania po lewej stronie, wybierz **integracji katalogów**.
2. Przejdź toohello **synchronizacji** kartę.
3. U dołu hello wybierz **Dodaj**
4. W hello **Dodawanie elementu synchronizacji** wyświetlonym oknie Wybierz hello domeny, jednostki Organizacyjnej **lub** grupy zabezpieczeń, ustawienia domyślne metody i języka ustawienia domyślne dla tej synchronizacji zadań, a następnie kliknij przycisk **Dodaj**.
5. Pole hello wyboru **Włącz synchronizację z usługą Active Directory** i wybierz polecenie **interwał synchronizacji** od jednej minuty do 24 godzin.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Jak powitania serwera usługi Azure Multi-Factor Authentication obsługuje dane użytkownika

Gdy używasz powitania serwera Multi-Factor Authentication (MFA) na lokalnym dane użytkownika są przechowywane w serwery lokalne powitania. Brak danych trwałych użytkownika są przechowywane w chmurze hello. Gdy użytkownik hello przeprowadza weryfikację dwuetapową, powitania serwera usługi MFA wysyła toohello danych usługi Azure MFA chmury usługi tooperform hello weryfikacji. Te żądania uwierzytelnienia wysyłane toohello usługi w chmurze, hello następujące pola są wysyłane żądania hello i dzienniki, aby były dostępne w raportach użycia/uwierzytelniania powitania klienta. Niektóre pola hello są opcjonalne, dlatego są one włączone lub wyłączone w ramach hello aplikacji serwer Multi-Factor Authentication. komunikat Hello hello usługi w chmurze MFA toohello serwera usługi MFA używa protokołu SSL/TLS przez port 443 dla ruchu wychodzącego. Wysyłane mogą być następujące pola:

* Unikatowy identyfikator — nazwa użytkownika lub wewnętrzny identyfikator serwera MFA
* Imię i nazwisko (opcjonalnie)
* Adres e-mail (opcjonalnie)
* Numer telefonu — używany w trakcie uwierzytelniania za pomocą połączenia głosowego lub wiadomości SMS
* Tokenu urządzenia — używany podczas uwierzytelniania za pomocą aplikacji mobilnej
* Tryb uwierzytelniania
* Wynik uwierzytelniania
* Nazwa serwera MFA
* Adres IP serwera MFA
* Adres IP klienta — jeśli jest dostępny

Toohello powyższych pól, wynik weryfikacji hello (Powodzenie/odmowa) i przyczynę żadnych Odmów jest ponadto również przechowywane z danymi uwierzytelniania hello i dostępne za pośrednictwem uwierzytelniania hello/raporty.

## <a name="back-up-and-restore-azure-mfa-server"></a>Tworzenie kopii zapasowej serwera usługi Azure MFA i jej przywracanie

Upewniając się, że masz dobrej kopii zapasowej jest tootake ważnym krokiem w dowolnym systemie.

tooback się serwera usługi Azure MFA, upewnij się, że masz kopię hello **C:\Program Files\Multi-Factor Authentication Server\Data** folderu, w tym hello **PhoneFactor.pfdata** pliku. 

W przypadku a przywracania jest wymagana pełna hello następujące kroki:

1. Ponownie zainstaluj serwer usługi Azure MFA na nowym serwerze.
2. Aktywuj hello nowego serwera usługi Azure MFA.
3. Zatrzymaj hello **MultiFactorAuth** usługi.
4. Zastąp hello **PhoneFactor.pfdata** z hello kopii zapasowej.
5. Uruchom hello **MultiFactorAuth** usługi.

nowy serwer Hello jest teraz uruchomiona z hello oryginalnej kopii zapasowej konfiguracji i danych użytkowników.

## <a name="next-steps"></a>Następne kroki

- Instalowanie i konfigurowanie hello [Portal użytkowników](multi-factor-authentication-get-started-portal.md) dla użytkownika samoobsługi.
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [usługi federacyjne Active Directory](multi-factor-authentication-get-started-adfs.md), [uwierzytelnianie usługi RADIUS](multi-factor-authentication-get-started-server-radius.md), lub [uwierzytelniania LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalowanie i konfigurowanie [bramy usług pulpitu zdalnego i serwera Azure Multi-Factor Authentication korzystających z usługi RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Wdrażanie hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).
- [Zaawansowane scenariusze obejmujące usługę Azure Multi-Factor Authentication i sieci VPN innych firm](multi-factor-authentication-advanced-vpn-configurations.md).
