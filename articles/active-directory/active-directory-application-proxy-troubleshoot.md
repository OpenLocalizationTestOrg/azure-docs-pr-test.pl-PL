---
title: "Rozwiązywanie problemów z serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Opisano sposoby rozwiązywania problemów w serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 3ef74c8d5d5b75eb2bca4e6c994f4718b5226db8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Rozwiązywanie problemów z serwera Proxy aplikacji i komunikaty o błędach
Jeśli wystąpi błąd podczas uzyskiwania dostępu do opublikowanych aplikacji lub w przypadku publikowania aplikacji, sprawdź następujące opcje, aby zobaczyć, czy serwer Proxy aplikacji usługi AD Microsoft Azure działa poprawnie:

* Otwórz konsolę usług systemu Windows i sprawdź, czy **łącznik serwera Proxy aplikacji usługi Microsoft AAD** usługi jest włączona i uruchomiona. Możesz spojrzeć na stronie właściwości serwera Proxy aplikacji usługi jak pokazano na poniższej ilustracji:  
  ![Zrzut ekranu okna właściwości łącznika serwera Proxy aplikacji usługi Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Otwórz Podgląd zdarzeń i poszukaj zdarzeń łącznika serwera Proxy aplikacji w **Dzienniki aplikacji i usług** > **Microsoft** > **AadApplicationProxy**  >  **Łącznik** > **Admin**.
* W razie potrzeby bardziej szczegółowe dzienniki są dostępne przez [Włączanie dzienników sesji łącznika serwera Proxy aplikacji](application-proxy-understand-connectors.md#under-the-hood).

Aby uzyskać więcej informacji o narzędziu Azure AD Rozwiązywanie problemów, zobacz [narzędzia do rozwiązywania problemów do sprawdzania wymagań wstępnych sieci łącznika](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="the-page-is-not-rendered-correctly"></a>Strony nie są odtwarzane poprawnie
Mogą wystąpić problemy z aplikacją renderowania lub działać poprawnie bez otrzymania określone komunikaty o błędach. Może to wystąpić, jeśli opublikowane Ścieżka artykułu, ale aplikacja wymaga zawartości znajdujących się poza tej ścieżki.

Na przykład jeśli publikowanie https://yourapp/app ścieżki, ale aplikacja wywołuje obrazów w https://yourapp/media, ich nie być renderowane. Upewnij się, że publikowanie aplikacji przy użyciu najwyższego poziomu ścieżki należy uwzględnić wszystkie odpowiedniej zawartości. W tym przykładzie byłoby http://yourapp/.

W przypadku zmiany ścieżki uwzględnić zawartość, której dotyczy odwołanie, ale mimo to muszą użytkownikom trafić na bardziej łącze w ścieżce, zobacz wpis w blogu [ustawienie łącze prawym dla aplikacji serwera Proxy aplikacji w usłudze Azure AD dostęp panelu i uruchamianie aplikacji usługi Office 365](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Błędy łącznika

Użyj [Azure AD aplikacji serwera Proxy łącznika porty testu narzędzia](https://aadap-portcheck.connectorporttest.msappproxy.net/) można zweryfikować, że Twoje łącznika może nawiązać połączenie usługi Serwer Proxy aplikacji. Co najmniej upewnij się, że region środkowe stany USA i najbliższego region jest wszystkich zielony zaznaczeń. Ponadto więcej zaznaczeń zielony oznacza większą elastyczność. 

Jeśli rejestracja łącznika Kreator instalacji zakończy się niepowodzeniem, istnieją dwa sposoby wyświetlania przyczynę błędu. Albo poszukaj w dzienniku zdarzeń w obszarze **aplikacji i usług Logs\Microsoft\AadApplicationProxy\Connector\Admin**, lub uruchom następujące polecenie programu Windows PowerShell:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Po znalezieniu błąd łącznika z dziennika zdarzeń Użyj tej tabeli typowych błędów, aby rozwiązać ten problem:

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Rejestracja łącznika nie powiodła się: Upewnij się, że włączono serwer Proxy aplikacji w portalu zarządzania Azure i podana poprawna nazwa użytkownika usługi Active Directory i hasło. Błąd: "co najmniej jeden błąd." | Po zamknięciu okna rejestracji bez rejestrowania się w usłudze Azure AD, uruchom ponownie Kreatora łącznika i rejestrowanie łącznika. <br><br> Jeśli okno rejestracji zostanie otwarty i natychmiast zamknie bez zezwalania na można się zalogować, prawdopodobnie otrzyma ten błąd. Ten błąd występuje, gdy występuje błąd sieci w Twoim systemie. Upewnij się, czy jest możliwe do nawiązania połączenia z przeglądarką publicznej witrynie sieci Web i że porty są otwarte, jak określono w [wymagania wstępne serwera Proxy aplikacji](active-directory-application-proxy-enable.md). |
| Wyczyść błędu jest podana w oknie rejestracji. Nie można kontynuować | Jeśli zostanie wyświetlony ten błąd, a następnie zamyka okno, wprowadzono nieprawidłową nazwę użytkownika lub hasło. Próbuj ponownie. |
| Rejestracja łącznika nie powiodła się: Upewnij się, że włączono serwer Proxy aplikacji w portalu zarządzania Azure i podana poprawna nazwa użytkownika usługi Active Directory i hasło. Błąd: "AADSTS50059: żadne informacje identyfikujące dzierżawy znaleziony w jednym żądaniu lub implikowana przez wszelkie wprowadzone poświadczenia i wyszukiwania przez usługę główną identyfikatora URI nie powiodła się. | Próbujesz zalogować się przy użyciu Account Microsoft i nie będącej częścią identyfikator organizacji w katalogu, który próbujesz uzyskać dostęp do domeny. Upewnij się, że administrator jest częścią tej samej nazwy domeny, jak domena dzierżawy, na przykład, jeśli domena usługi Azure AD to contoso.com, administrator powinien mieć admin@contoso.com. |
| Nie można pobrać bieżące zasady wykonywania dla uruchomionych skryptów PowerShell. | Jeśli instalacja łącznika nie powiedzie się, sprawdź, upewnij się, że zasady wykonywania programu PowerShell nie jest wyłączone. <br><br>1. Otwórz Edytor zasad grupy.<br>2. Przejdź do **Konfiguracja komputera** > **Szablony administracyjne** > **składniki systemu Windows**  >   **Środowisko Windows PowerShell** i kliknij dwukrotnie **włączyć wykonywanie skryptów**.<br>3. Zasady wykonywania może być ustawiona jako **nieskonfigurowane** lub **włączone**. Jeśli ustawiono **włączone**, upewnij się, że w obszarze Opcje, zasady wykonywania jest ustawiona jako **Zezwalaj lokalnego i zdalnego podpisanych skryptów** lub **wszystkie skrypty**. |
| Nie można pobrać konfiguracji łącznika. | Certyfikat klienta łącznika, który jest używany do uwierzytelniania, wygasł. To może również wystąpić, jeśli masz zainstalowanego za serwerem proxy łącznika. W takim przypadku łącznik nie może uzyskać dostęp do Internetu i nie będzie mógł udostępnianie aplikacji użytkownikom zdalnym. Odnowić ręcznie za pomocą `Register-AppProxyConnector` polecenia cmdlet programu Windows PowerShell. Jeśli Twoje łącznika jest za serwerem proxy, należy przyznać dostęp do Internetu dla konta łącznika "usługi sieciowej" i "system lokalny". Można to osiągnąć, umożliwiając im dostępu do serwera Proxy lub przez ustawienie je, aby pominąć serwer proxy. |
| Rejestracja łącznika nie powiodła się: Upewnij się, że jesteś administratorem globalnym usługi Active Directory, aby zarejestrować łącznika. Błąd: "rejestracji żądanie zostało odrzucone." | Alias, który próbuje zalogować się przy użyciu nie jest administratorem tej domeny. Twoje łącznika jest zawsze instalowany w katalogu, który jest właścicielem domeny użytkownika. Upewnij się, że konto administratora, z którym próbujesz się zalogować ma uprawnienia globalne do dzierżawy usługi Azure AD. |

## <a name="kerberos-errors"></a>Błędy protokołu Kerberos

Ta tabela obejmuje więcej typowych błędów, które pochodzą z protokołu Kerberos i Konfiguracja i zawiera sugestie dotyczące rozwiązania.

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Nie można pobrać bieżące zasady wykonywania dla uruchomionych skryptów PowerShell. | Jeśli instalacja łącznika nie powiedzie się, sprawdź, upewnij się, że zasady wykonywania programu PowerShell nie jest wyłączone.<br><br>1. Otwórz Edytor zasad grupy.<br>2. Przejdź do **Konfiguracja komputera** > **Szablony administracyjne** > **składniki systemu Windows**  >   **Środowisko Windows PowerShell** i kliknij dwukrotnie **włączyć wykonywanie skryptów**.<br>3. Zasady wykonywania może być ustawiona jako **nieskonfigurowane** lub **włączone**. Jeśli ustawiono **włączone**, upewnij się, że w obszarze Opcje, zasady wykonywania jest ustawiona jako **Zezwalaj lokalnego i zdalnego podpisanych skryptów** lub **wszystkie skrypty**. |
| 12008 — usługi azure AD Przekroczono maksymalną liczbę dozwolonych prób uwierzytelnienia Kerberos do serwera wewnętrznej bazy danych. | Ten błąd może wskazywać niepoprawną konfiguracją między usługą Azure AD i serwera wewnętrznej bazy danych aplikacji lub na problem w konfiguracji Data i godzina na obu komputerach. Serwer wewnętrznej bazy danych odrzucił bilet Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza są skonfigurowane poprawnie. Upewnij się, że data i godzina konfiguracji usługi Azure AD, a serwer aplikacji zaplecza są synchronizowane. |
| 13016 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika, ponieważ nie istnieje żadne nazwy UPN w tokenie granicznym lub w pliku cookie dostępu. | Istnieje problem z konfiguracją usługi STS. Usuń konfigurację oświadczenia UPN w usługi STS. |
| 13019 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika z powodu następującego błędu ogólnego interfejsu API. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD, a serwer kontrolera domeny lub problem w konfiguracji Data i godzina na obu komputerach. Kontroler domeny odrzucił bilet Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza są skonfigurowane poprawnie, szczególnie konfiguracji głównej nazwy usługi. Upewnij się, że usługi Azure AD jest przyłączony do tej samej domenie co kontroler domeny, aby upewnić się, że kontroler domeny ustanawia relację zaufania z usługą Azure AD. Upewnij się, że data i godzina konfiguracji usługi Azure AD i są synchronizowane z kontrolerem domeny. |
| 13020 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika, ponieważ nazwa SPN serwera wewnętrznej bazy danych nie jest zdefiniowany. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD, a serwer kontrolera domeny lub problem w konfiguracji Data i godzina na obu komputerach. Kontroler domeny odrzucił bilet Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza są skonfigurowane poprawnie, szczególnie konfiguracji głównej nazwy usługi. Upewnij się, że usługi Azure AD jest przyłączony do tej samej domenie co kontroler domeny, aby upewnić się, że kontroler domeny ustanawia relację zaufania z usługą Azure AD. Upewnij się, że data i godzina konfiguracji usługi Azure AD i są synchronizowane z kontrolerem domeny. |
| 13022 — usługi azure AD nie można uwierzytelnić użytkownika, ponieważ serwer wewnętrznej bazy danych odpowiada prób uwierzytelnienia Kerberos z powodu błędu HTTP 401. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD i serwera wewnętrznej bazy danych aplikacji lub na problem w konfiguracji Data i godzina na obu komputerach. Serwer wewnętrznej bazy danych odrzucił bilet Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza są skonfigurowane poprawnie. Upewnij się, że data i godzina konfiguracji usługi Azure AD, a serwer aplikacji zaplecza są synchronizowane. |

## <a name="end-user-errors"></a>Błędy użytkownika końcowego

Ta lista zawiera błędy, które użytkownicy końcowi mogą napotkać podczas próby dostępu do aplikacji i zakończyć się niepowodzeniem. 

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Witryna sieci Web nie można wyświetlić strony. | Błąd ten może wystąpić użytkownika, podczas próby uzyskania dostępu do aplikacji, która została opublikowana, gdy aplikacja jest aplikacja IWA. Zdefiniowane nazwy SPN dla tej aplikacji może być nieprawidłowa. Dla aplikacji IWA upewnij się, czy nazwa SPN skonfigurowane dla tej aplikacji jest prawidłowa. |
| Witryna sieci Web nie można wyświetlić strony. | Błąd ten może wystąpić użytkownika, podczas próby uzyskania dostępu do aplikacji, która została opublikowana, gdy aplikacja jest aplikacja usługi OWA. Może to być spowodowane jedną z następujących:<br><li>Zdefiniowane nazwy SPN dla tej aplikacji jest niepoprawna. Upewnij się, czy nazwa SPN skonfigurowane dla tej aplikacji jest prawidłowa.</li><li>Użytkownik próbował uzyskać dostęp do aplikacji jest za pomocą konta Microsoft, a nie prawidłowego konta firmowego, logować się lub użytkownik jest użytkownikiem gościa. Upewnij się, że użytkownik loguje się przy użyciu ich konta firmowego, który pasuje do domeny opublikowanej aplikacji. Użytkownicy Account firmy Microsoft, jak i gościa nie może uzyskiwać dostęp do aplikacji IWA.</li><li>Użytkownik próbował uzyskać dostęp do aplikacji nie jest poprawnie zdefiniowany dla tej aplikacji po stronie lokalnego. Upewnij się, że ten użytkownik ma odpowiednie uprawnienia zdefiniowane dla tej aplikacji zaplecza na maszynie lokalnej. |
| Nie można uzyskać dostępu do tej aplikacji firmowych. Nie masz uprawnień dostępu do tej aplikacji. Autoryzacja nie powiodła się. Upewnij się przypisać użytkownika z dostępem do tej aplikacji. | Błąd ten może wystąpić użytkowników, podczas próby uzyskania dostępu do aplikacji, która została opublikowana, jeśli używają kont Microsoft do logowania zamiast koncie firmowym. Błąd ten może również wystąpić gości. Użytkownicy Account firmy Microsoft i gości nie może uzyskiwać dostęp do aplikacji IWA. Upewnij się, że użytkownik loguje się przy użyciu ich konta firmowego, który pasuje do domeny opublikowanej aplikacji.<br><br>Może nie przypisano użytkowników dla tej aplikacji. Przejdź do **aplikacji** kartę, a następnie w obszarze **użytkowników i grup**, przypisz tego użytkownika lub grupy użytkowników do tej aplikacji. |
| Ta aplikacja firmy nie jest dostępny w tej chwili. Spróbuj ponownie później... Łącznik został przekroczony. | Błąd ten może wystąpić użytkowników, podczas próby uzyskania dostępu do aplikacji, która została opublikowana, jeśli ich nie zostały poprawnie zdefiniowane dla tej aplikacji po stronie lokalnego. Upewnij się, czy użytkownicy mają odpowiednie uprawnienia, zgodnie z definicją dla tej aplikacji zaplecza na maszynie lokalnej. |
| Nie można uzyskać dostępu do tej aplikacji firmowych. Nie masz uprawnień dostępu do tej aplikacji. Autoryzacja nie powiodła się. Upewnij się, że użytkownik ma licencję dla usługi Azure Active Directory — wersja Premium lub Basic. | Błąd ten może wystąpić użytkowników, podczas próby uzyskania dostępu do aplikacji, która została opublikowana, jeśli nie zostały one jawnie przypisane z licencją podstawową/Premium przez administratora abonenta. Przejdź do usługi Active Directory abonenta **licencji** karcie i upewnij się, że ten użytkownik lub grupa użytkowników ma przypisanej licencji wersji Premium lub podstawowa. |

## <a name="my-error-wasnt-listed-here"></a>Mój błąd nie zostało przedstawione w tym miejscu

Jeśli wystąpi błąd lub problem z aplikacji serwera Proxy Azure AD, która nie ma na liście w tym przewodniku rozwiązywania problemów, chcielibyśmy usłyszeć informacji na ten temat. Wyślij wiadomość e-mail do naszej [zespołu opinii](mailto:aadapfeedback@microsoft.com) szczegółowe informacje o błędzie.

## <a name="see-also"></a>Zobacz też
* [Włącz serwer Proxy aplikacji usługi Azure Active Directory](active-directory-application-proxy-enable.md)
* [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-publish.md)
* [Włącz rejestrację jednokrotną](active-directory-application-proxy-sso-using-kcd.md)
* [Włączanie dostępu warunkowego](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
