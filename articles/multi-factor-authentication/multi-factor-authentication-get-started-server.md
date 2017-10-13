---
title: Wprowadzenie do serwera Azure Multi-Factor Authentication | Microsoft Docs
description: "Ta strona dotycząca usługi Azure Multi-Factor Authentication zawiera informacje umożliwiające rozpoczęcie korzystania z serwera Azure MFA."
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
ms.date: 08/30/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: df847c370817c0702163b5e22c35c7e4f1d3cfee
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="getting-started-with-the-azure-multi-factor-authentication-server"></a>Wprowadzenie do serwera Azure Multi-Factor Authentication

<center>![Lokalna usługa MFA](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Po podjęciu decyzji o użyciu lokalnego serwera Multi-Factor Authentication można przejść do kolejnych kroków. Ta strona obejmuje nową instalację serwera oraz jego konfigurację z uwzględnieniem lokalnej usługi Active Directory. Jeśli masz już zainstalowany serwer MFA i chcesz go uaktualnić, zobacz [Upgrade to the latest Azure Multi-Factor Authentication Server](multi-factor-authentication-server-upgrade.md) (Uaktualnianie do najnowszej wersji serwera Azure Multi-Factor Authentication). Jeśli szukasz informacji dotyczących instalowania tylko usługi sieci Web, zobacz [Wdrażanie usługi sieci Web aplikacji mobilnej serwera Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planowanie wdrożenia

Przed pobraniem serwera Azure Multi-Factor Authentication zastanów się, jakie są wymagania w zakresie obciążenia i wysokiej dostępności. Te informacje pozwolą podjąć decyzję dotyczącą sposobu i miejsca wdrożenia.

Wskazówką dotyczącą ilości wymaganej pamięci jest przewidywana liczba użytkowników, którzy będą regularnie się uwierzytelniać.

| Użytkownicy | Pamięć RAM |
| ----- | --- |
| 1–10 000 | 4 GB |
| 10 001–50 000 | 8 GB |
| 50 001–100 000 | 12 GB |
| 100 000–200 001 | 16 GB |
| 200 001+ | 32 GB |

Czy trzeba skonfigurować wiele serwerów w celu zapewnienia wysokiej dostępności lub równoważenia obciążenia? Istnieje szereg sposobów uzyskania takiej konfiguracji przy użyciu serwera Azure MFA. Pierwszy zainstalowany serwer Azure MFA staje się serwerem głównym. Wszelkie dodatkowe serwery są podrzędne i automatycznie synchronizują użytkowników i konfigurację z serwerem głównym. Następnie można skonfigurować jeden serwer podstawowy, a resztę jako serwery kopii zapasowej. Można też skonfigurować równoważenie obciążenia na wszystkich serwerach.

Jeśli serwer główny Azure MFA przejdzie do trybu offline, serwery podrzędne wciąż mogą przetwarzać żądania weryfikacji dwuetapowej. Jednak nie można wtedy dodawać nowych użytkowników, a istniejący użytkownicy nie mogą aktualizować ustawień, chyba że serwer główny powróci do trybu online lub zostanie podwyższony poziom serwera podrzędnego.

### <a name="prepare-your-environment"></a>Przygotowywanie środowiska

Upewnij się, że serwer Azure Multi-Factor Authentication spełnia następujące wymagania:

| Wymagania serwera Azure Multi-Factor Authentication | Opis |
|:--- |:--- |
| Sprzęt |<li>200 MB wolnego miejsca na dysku twardym</li><li>Procesor umożliwiający obsługę architektury x32 lub x64</li><li>Co najmniej 1 GB pamięci RAM</li> |
| Oprogramowanie |<li>Windows Server 2016</li><li>Windows Server 2012 R2</li><li>Windows Server 2012</li><li>Windows Server 2008 R2</li><li>Windows Server 2008, z dodatkiem SP1, SP2</li><li>Windows Server 2003 R2</li><li>Windows Server 2003, z dodatkiem SP1, SP2</li><li>Windows 10</li><li>Windows 8.1, wszystkie wersje</li><li>Windows 8, wszystkie wersje</li><li>Windows 7, wszystkie wersje</li><li>Windows Vista, wszystkie wersje, z dodatkiem SP1, SP2</li><li>Oprogramowanie Microsoft .NET 4.0 Framework</li><li>Usługi IIS 7.0 lub nowsze w przypadku instalacji portalu użytkowników lub zestawu SDK usługi sieci Web</li> |

### <a name="azure-mfa-server-components"></a>Składniki serwera usługi Azure MFA

W skład serwera usługi Azure MFA wchodzą trzy składniki internetowe:

* Zestaw SDK usługi internetowej — umożliwia komunikację z innymi składnikami i jest instalowany na serwerze aplikacji usługi Azure MFA
* Portal użytkowników — witryna internetowa usług IIS, dzięki której użytkownicy mogą zarejestrować się w usłudze Azure Multi-Factor Authentication (MFA) i obsługiwać swoje konta.
* Usługa internetowa aplikacji mobilnych — umożliwia korzystanie z aplikacji mobilnej, takiej jak aplikacja Microsoft Authenticator, w celu przeprowadzenia weryfikacji dwuetapowej.

Wszystkie trzy składniki można zainstalować na jednym serwerze, jeśli jest to serwer dostępny z Internetu. W przypadku rozdzielania składników zestaw SDK usługi internetowej jest instalowany na serwerze aplikacji usługi Azure MFA, a portal użytkowników i usługa internetowa aplikacji mobilnych — na serwerze dostępnym z Internetu.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Wymagania serwera Azure Multi-Factor Authentication dotyczące zapory

Każdy serwer MFA musi mieć możliwość komunikacji wychodzącej za pośrednictwem portu 443 z następującymi adresami:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Jeśli zapory ruchu wychodzącego mają ograniczenie na porcie 443, otwórz następujące zakresy adresów IP:

| Podsieć IP | Maska sieci | Zakres adresów IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Jeśli nie używasz funkcji potwierdzania zdarzeń i użytkownicy nie korzystają z uwierzytelniania z użyciem aplikacji mobilnych z poziomu urządzeń w sieci firmowej, potrzebujesz tylko następujących zakresów:

| Podsieć IP | Maska sieci | Zakres adresów IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-the-azure-multi-factor-authentication-server"></a>Pobieranie serwera Azure Multi-Factor Authentication

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) jako administrator.
2. W obszarze po lewej stronie wybierz pozycję **Active Directory**
3. Kliknij pozycję **Użytkownicy i grupy**
4. Kliknij pozycję **Wszyscy użytkownicy**
5. Kliknij pozycję **Multi-Factor Authentication**
6. W obszarze **uwierzytelniania wieloskładnikowego** wybierz pozycję **ustawienia usługi**

   ![Strona Ustawienia usługi](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Na stronie ustawień usługi, w dolnej części ekranu, kliknij opcję **Przejdź do portalu**. Zostanie otwarta nowa strona.
7. Kliknij pozycję **Pliki do pobrania**.
8. Kliknij link **Pobierz** link i zapisz instalator.

   ![Pobieranie serwera usługi MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Nie zamykaj tej strony, ponieważ będziemy odwoływać się do niej po uruchomieniu instalatora.

## <a name="install-and-configure-the-azure-multi-factor-authentication-server"></a>Instalowanie i konfigurowanie serwera usługi Azure Multi-Factor Authentication

Po pobraniu serwera możesz go zainstalować i skonfigurować. Sprawdź, czy serwer, na którym zamierzasz go zainstalować, spełnia wymagania podane w sekcji dotyczącej planowania.

1. Kliknij dwukrotnie plik wykonywalny.
2. Upewnij się, że na ekranie Wybieranie folderu instalacji wybrany jest prawidłowy folder, a następnie kliknij przycisk **Dalej**.
3. Po ukończeniu instalacji kliknij przycisk **Zakończ**.  Spowoduje to uruchomienie kreatora konfiguracji.
4. Na ekranie powitalnym kreatora konfiguracji zaznacz pole **Pomiń korzystanie z kreatora konfiguracji uwierzytelniania** i kliknij przycisk **Dalej**.  Spowoduje to zamknięcie kreatora i uruchomienie serwera.

   ![Chmura](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Na stronie, z której został pobrany serwer, kliknij przycisk **Generuj poświadczenia aktywacji**. Skopiuj uzyskane informacje do serwera Azure MFA, wpisując je w odpowiednich polach, a następnie kliknij przycisk **Aktywuj**.

## <a name="send-users-an-email"></a>Wysyłanie wiadomości e-mail do użytkowników

Aby ułatwić wprowadzenie, zezwól serwerowi usługi MFA na komunikowanie się z użytkownikami. Serwer MFA może wysłać wiadomość e-mail w celu poinformowania użytkowników o zarejestrowaniu ich na potrzeby weryfikacji dwuetapowej.

Wiadomość e-mail powinna zależeć od konfiguracji użytkowników na potrzeby weryfikacji dwuetapowej. Jeśli na przykład uda się zaimportować numery telefonów z katalogu firmy, wiadomość e-mail powinna zawierać domyślny numer telefonu, aby użytkownicy wiedzieli, czego oczekiwać. Jeśli nie importujesz numerów telefonów lub użytkownicy będą korzystać z aplikacji mobilnej, wyślij wiadomość e-mail umożliwiającą im ukończenie rejestracji konta. W wiadomości e-mail podaj hiperlink do portalu użytkownika usługi Azure Multi-Factor Authentication.

Treść wiadomości e-mail różni się też w zależności od metody weryfikacji, która została ustawiona dla użytkownika (połączenie telefoniczne, wiadomość SMS lub aplikacja mobilna).  Jeśli na przykład użytkownik musi podczas uwierzytelniania użyć numeru PIN, w wiadomości e-mail zostanie podany początkowy numer PIN.  Użytkownicy muszą zmienić numer PIN podczas pierwszej weryfikacji.

### <a name="configure-email-and-email-templates"></a>Konfigurowanie wiadomości e-mail i szablonów wiadomości e-mail

Kliknij ikonę poczty e-mail z lewej strony, aby skonfigurować ustawienia wysyłania tych wiadomości e-mail. Na tej stronie można wprowadzić dane SMTP serwera poczty oraz wysyłać wiadomości e-mail przez zaznaczenie pola wyboru **Wyślij wiadomości e-mail do użytkowników**.

![Konfiguracja poczty e-mail serwera usługi MFA](./media/multi-factor-authentication-get-started-server/email1.png)

Na karcie Zawartość wiadomości e-mail są widoczne szablony wiadomości e-mail, które są dostępne do wyboru. W zależności od ustawień weryfikacji dwuetapowej skonfigurowanych dla użytkowników można wybrać szablon najlepiej odpowiadający bieżącym potrzebom.

![Szablony poczty e-mail serwera usługi MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importowanie użytkowników z usługi Active Directory

Teraz, po zainstalowaniu serwera, należy dodać użytkowników. Możesz utworzyć ich ręcznie, zaimportować użytkowników z usługi Active Directory lub skonfigurować automatyczną synchronizację z usługą Active Directory.

### <a name="manual-import-from-active-directory"></a>Ręczne importowanie z usługi Active Directory

1. Na serwerze Azure MFA, w obszarze po lewej stronie, wybierz pozycję **Użytkownicy**.
2. U dołu ekranu wybierz pozycję **Importuj z usługi Active Directory**.
3. Po wykonaniu tych czynności możesz wyszukiwać poszczególnych użytkowników lub wyszukać w katalogu usługi AD jednostki organizacyjne obejmujące użytkowników.  W tym przypadku jest określana jednostka organizacyjna użytkowników.
4. Zaznacz wszystkich użytkowników po prawej stronie, a następnie kliknij przycisk **Importuj**.  Zostanie wyświetlone okno podręczne informujące, że proces został zakończony pomyślnie.  Zamknij okno importu.

   ![Importowanie użytkowników serwera usługi MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Automatyczna synchronizacja z usługą Active Directory

1. Na serwerze usługi Azure MFA, w obszarze po lewej stronie, wybierz pozycję **Integracja katalogu**.
2. Przejdź do karty **Synchronizacja**.
3. W dolnej części wybierz pozycję **Dodaj**
4. W wyświetlonym oknie **Dodawanie elementu synchronizacji** wybierz domenę, jednostkę organizacyjną **lub** grupę zabezpieczeń, ustawienia, wartości domyślne metody i wartości domyślne języka dla tego zadania synchronizacji, a następnie kliknij pozycję **Dodaj**.
5. Sprawdź pole o nazwie **Włącz synchronizację z usługą Active Directory** i wybierz **interwał synchronizacji** od jednej minuty do 24 godzin.

## <a name="how-the-azure-multi-factor-authentication-server-handles-user-data"></a>Sposób obsługi danych użytkowników przez serwer Azure Multi-Factor Authentication

W przypadku lokalnego użycia serwera Multi-Factor Authentication (MFA) dane użytkownika są przechowywane na serwerach lokalnych. Żadne trwałe dane użytkowników nie są przechowywane w chmurze. Gdy użytkownik przeprowadza weryfikację dwuetapową, serwer MFA wysyła dane do usługi Azure MFA w chmurze w celu przeprowadzenia weryfikacji. Podczas przesyłania żądań uwierzytelnienia do usługi w chmurze następujące pola są wysyłane w żądaniu i dziennikach, dzięki czemu są one dostępne w ramach raportów klienta dotyczących uwierzytelniania/użycia. Niektóre pola są opcjonalne i można je włączyć lub wyłączyć na serwerze Multi-Factor Authentication. Na potrzeby przesyłania danych z serwera MFA do usługi MFA w chmurze używany jest protokół SSL/TLS i port wyjściowy 443. Wysyłane mogą być następujące pola:

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

Oprócz powyższych pól wraz z danymi uwierzytelniania są przechowywane także wyniki weryfikacji (powodzenie/odmowa) oraz przyczyny odmów. Informacje te są potem dostępne w raportach dotyczących uwierzytelniania/użycia.

## <a name="back-up-and-restore-azure-mfa-server"></a>Tworzenie kopii zapasowej serwera usługi Azure MFA i jej przywracanie

Sprawdzenie, czy masz dobrą kopię zapasową, jest ważnym krokiem do wykonania w dowolnym systemie.

Aby utworzyć kopię zapasową serwera usługi Azure MFA, upewnij się, że masz kopię folderu **C:\Program Files\Multi-Factor Authentication Server\Data**, w tym pliku **PhoneFactor.pfdata**. 

Jeśli trzeba przywrócić dane, wykonaj następujące kroki:

1. Ponownie zainstaluj serwer usługi Azure MFA na nowym serwerze.
2. Aktywuj nowy serwer usługi Azure MFA.
3. Zatrzymaj usługę **MultiFactorAuth**.
4. Zastąp plik **PhoneFactor.pfdata** plikiem z kopii zapasowej.
5. Uruchom usługę **MultiFactorAuth**.

Nowy serwer jest teraz gotowy i został uruchomiony przy użyciu oryginalnych danych konfiguracji i użytkowników z kopii zapasowej.

## <a name="next-steps"></a>Następne kroki

- Instalowanie i konfigurowanie [portalu użytkowników](multi-factor-authentication-get-started-portal.md) dla użytkownika samoobsługi.
- Instalowanie i konfigurowanie serwera usługi Azure MFA przy użyciu [usług Active Directory Federation Services](multi-factor-authentication-get-started-adfs.md), [uwierzytelniania usługi RADIUS](multi-factor-authentication-get-started-server-radius.md) lub [uwierzytelniania LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalowanie i konfigurowanie [bramy usług pulpitu zdalnego i serwera Azure Multi-Factor Authentication korzystających z usługi RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Wdrażanie usługi sieci Web aplikacji mobilnej serwera Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server-webservice.md).
- [Zaawansowane scenariusze obejmujące usługę Azure Multi-Factor Authentication i sieci VPN innych firm](multi-factor-authentication-advanced-vpn-configurations.md).
