---
title: Serwer Proxy aplikacji aaaTroubleshoot | Dokumentacja firmy Microsoft
description: "Obejmuje jak błędy tootroubleshoot serwera Proxy aplikacji usługi Azure AD."
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
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Rozwiązywanie problemów z serwera Proxy aplikacji i komunikaty o błędach
Jeśli wystąpi błąd podczas uzyskiwania dostępu do opublikowanych aplikacji lub w przypadku publikowania aplikacji, sprawdź następujące opcje toosee, jeśli serwer Proxy aplikacji usługi AD Microsoft Azure działa prawidłowo hello:

* Usługi Windows hello Otwórz konsoli i sprawdź, że hello **łącznik serwera Proxy aplikacji usługi Microsoft AAD** usługi jest włączona i uruchomiona. Można również toolook na stronie właściwości usługi Serwer Proxy aplikacji hello, jak pokazano w powitania po obrazu:  
  ![Zrzut ekranu okna właściwości łącznika serwera Proxy aplikacji usługi Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Otwórz Podgląd zdarzeń i poszukaj zdarzeń łącznika serwera Proxy aplikacji w **Dzienniki aplikacji i usług** > **Microsoft** > **AadApplicationProxy**  >  **Łącznik** > **Admin**.
* W razie potrzeby bardziej szczegółowe dzienniki są dostępne przez [włączenie hello dzienniki sesji łącznika serwera Proxy aplikacji](application-proxy-understand-connectors.md#under-the-hood).

Aby uzyskać więcej informacji na temat narzędzia do rozwiązywania problemów hello Azure AD, zobacz [Rozwiązywanie problemów z sieci wymagania wstępne narzędzia toovalidate łącznik](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>Strona Hello nie są odtwarzane poprawnie
Mogą wystąpić problemy z aplikacją renderowania lub działać poprawnie bez otrzymania określone komunikaty o błędach. Może to wystąpić, jeśli opublikowane Ścieżka artykułu hello, ale aplikacja hello wymaga zawartości znajdujących się poza tej ścieżki.

Na przykład jeśli publikowanie hello https://yourapp/app ścieżki, ale aplikacja hello wywołuje obrazów w https://yourapp/media, ich nie być renderowane. Upewnij się, że publikowanie aplikacji hello przy użyciu ścieżki poziomu z najwyższym hello należy tooinclude wszystkie odpowiedniej zawartości. W tym przykładzie byłoby http://yourapp/.

Jeśli zmiany zawartości tooinclude odwołuje się do ścieżki, ale nadal potrzebujesz tooland użytkowników głębiej łącze w ścieżce hello, zobacz hello blogu [łącze prawym hello ustawienie dla aplikacji serwera Proxy aplikacji w panelu dostępu hello Azure AD i aplikacji usługi Office 365 uruchamianie](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Błędy łącznika

Użyj hello [Azure AD aplikacji serwera Proxy łącznika porty testu narzędzie](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify, że Twoje łącznika może nawiązać połączenie powitania serwera Proxy aplikacji usługi. Co najmniej upewnij się, że hello środkowe stany USA regionu i tooyou najbliższy region hello jest wszystkich zaznaczeń zielony. Ponadto więcej zaznaczeń zielony oznacza większą elastyczność. 

Jeśli rejestracja hello łącznika Kreator instalacji zakończy się niepowodzeniem, istnieją dwa sposoby tooview hello Przyczyna niepowodzenia hello. Szukaj albo w dzienniku zdarzeń hello w obszarze **aplikacji i usług Logs\Microsoft\AadApplicationProxy\Connector\Admin**, lub hello uruchom następujące polecenia programu Windows PowerShell:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Po znalezieniu hello łącznika błędu z dziennika zdarzeń hello, użyj tej tabeli typowe błędy tooresolve hello problemu:

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Rejestracja łącznika nie powiodła się: Upewnij się, że włączono serwer Proxy aplikacji w portalu zarządzania Azure hello i podana poprawna nazwa użytkownika usługi Active Directory i hasło. Błąd: "co najmniej jeden błąd." | Po zamknięciu okna rejestracji hello bez rejestrowania się w tooAzure AD, uruchom ponownie Kreatora łącznika hello i zarejestrować hello łącznika. <br><br> Jeśli okno Rejestracja hello otwiera, natychmiast zamknie bez zezwalania na toolog w będzie prawdopodobnie ten błąd. Ten błąd występuje, gdy występuje błąd sieci w Twoim systemie. Upewnij się, czy jest możliwe tooconnect z przeglądarki tooa publicznej witryny sieci Web i że hello porty są otwarte, jak określono w [wymagania wstępne serwera Proxy aplikacji](active-directory-application-proxy-enable.md). |
| Wyczyść błędu jest podana w hello okna rejestracji. Nie można kontynuować | Jeśli zostanie wyświetlony ten błąd, a następnie zamyka okno hello, wprowadzono hello nieprawidłową nazwą użytkownika lub hasło. Próbuj ponownie. |
| Rejestracja łącznika nie powiodła się: Upewnij się, że włączono serwer Proxy aplikacji w portalu zarządzania Azure hello i podana poprawna nazwa użytkownika usługi Active Directory i hasło. Błąd: "AADSTS50059: żadne informacje identyfikujące dzierżawy znaleziono w każdym żądaniu hello lub implikowana przez wszelkie wprowadzone poświadczenia i wyszukiwania przez usługę główną identyfikatora URI nie powiodła się. | Próbujesz toosign przy użyciu Account Microsoft i nie domeny, która jest częścią Identyfikatora organizacji hello katalogu hello próbujesz tooaccess. Upewnij się, że Witaj, Administratorze jest częścią hello tej samej nazwy domeny, jak domena dzierżawy hello, na przykład, jeśli domena hello Azure AD to contoso.com, Witaj, Administratorze powinna być admin@contoso.com. |
| Nie można tooretrieve hello bieżące zasady wykonywania uruchamiania skryptów środowiska PowerShell. | W przypadku niepowodzenia instalacji łącznika hello Sprawdź toomake się upewnić, że zasady wykonywania programu PowerShell nie jest wyłączone. <br><br>1. Witaj Otwórz Edytor zasad grupy.<br>2. Przejdź za**Konfiguracja komputera** > **Szablony administracyjne** > **składniki systemu Windows**  >   **Środowisko Windows PowerShell** i kliknij dwukrotnie **włączyć wykonywanie skryptów**.<br>3. można ustawić zasady wykonywania hello tooeither **nieskonfigurowane** lub **włączone**. Jeśli ustawiona zbyt**włączone**, upewnij się, że w obszarze Opcje, hello zasady wykonywania jest ustawiony tooeither **Zezwalaj lokalnego i zdalnego podpisanych skryptów** lub zbyt**wszystkie skrypty**. |
| Łącznik nie toodownload hello konfiguracji. | Łącznik powitania klienta certyfikatu, który jest używany do uwierzytelniania, wygasł. To może również wystąpić, jeśli masz hello zainstalowania łącznika za serwerem proxy. W takim przypadku hello łącznika nie ma dostępu do Internetu hello i nie będą mogli tooprovide aplikacji tooremote użytkowników. Odnowić ręcznie za pomocą hello `Register-AppProxyConnector` polecenia cmdlet programu Windows PowerShell. Jeśli Twojego łącznika znajduje się za serwerem proxy, jest niezbędne toogrant Internet access toohello łącznika kont "usługi sieciowej" i "system lokalny". Można to zrobić przez udzielanie dostępu ich toohello Proxy albo ustawiając ich toobypass hello serwera proxy. |
| Rejestracja łącznika nie powiodła się: Upewnij się, że jesteś administratorem globalnym hello tooregister użytkownika usługi Active Directory Connector. Błąd: "hello rejestracji żądanie zostało odrzucone." | Witaj alias, który próbujesz toolog przy użyciu nie jest administratorem tej domeny. Twoje łącznika jest zawsze instalowany w katalogu hello, który jest właścicielem domeny użytkownika hello. Upewnij się, że hello konto administratora, którą próbujesz toosign z dzierżawą uprawnień globalnych toohello usługi Azure AD. |

## <a name="kerberos-errors"></a>Błędy protokołu Kerberos

W tej tabeli podano hello częściej błędów, które pochodzą z protokołu Kerberos i konfiguracja, a także sugestie dotyczące rozpoznawania.

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Nie można tooretrieve hello bieżące zasady wykonywania uruchamiania skryptów środowiska PowerShell. | W przypadku niepowodzenia instalacji łącznika hello Sprawdź toomake się upewnić, że zasady wykonywania programu PowerShell nie jest wyłączone.<br><br>1. Witaj Otwórz Edytor zasad grupy.<br>2. Przejdź za**Konfiguracja komputera** > **Szablony administracyjne** > **składniki systemu Windows**  >   **Środowisko Windows PowerShell** i kliknij dwukrotnie **włączyć wykonywanie skryptów**.<br>3. można ustawić zasady wykonywania hello tooeither **nieskonfigurowane** lub **włączone**. Jeśli ustawiona zbyt**włączone**, upewnij się, że w obszarze Opcje, hello zasady wykonywania jest ustawiony tooeither **Zezwalaj lokalnego i zdalnego podpisanych skryptów** lub zbyt**wszystkie skrypty**. |
| 12008 - azure AD przekroczył hello maksymalną liczbę dozwolonych uwierzytelnianie Kerberos prób toohello serwera wewnętrznej bazy danych. | Ten błąd może wskazywać niepoprawną konfiguracją między usługą Azure AD i hello wewnętrznej bazy danych serwera aplikacji lub na problem w konfiguracji Data i godzina na obu komputerach. powitania serwera wewnętrznej bazy danych odrzucił bilet Kerberos hello utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza hello są skonfigurowane poprawnie. Upewnij się, konfiguracja Data i godzina hello na powitania usługi Azure AD i serwer aplikacji zaplecza hello są synchronizowane. |
| 13016 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika hello, ponieważ nie bez nazwy UPN w programie hello edge tokenu lub w pliku cookie dostępu hello. | Istnieje problem z konfiguracją usługi STS hello. Napraw hello oświadczenia UPN konfiguracji w hello STS. |
| 13019 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika hello ze względu na powitania po ogólny błąd interfejsu API. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD, a serwer kontrolera domeny hello, lub na problem w konfiguracji Data i godzina na obu komputerach. Kontroler domeny Hello odrzucone hello biletu Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza hello są poprawnie skonfigurowane, szczególnie hello SPN konfiguracji. Upewnij się, że hello Azure AD jest przyłączony do domeny toohello tej samej domeny, jak hello tooensure kontrolera domeny, który hello kontrolera domeny ustanawia relację zaufania z usługą Azure AD. Upewnij się, Data i godzina konfiguracji hello na powitania usługi Azure AD i kontroler domeny hello są synchronizowane. |
| 13020 — usługi azure AD nie można pobrać biletu protokołu Kerberos w imieniu użytkownika hello, ponieważ nazwa SPN serwera wewnętrznej bazy danych hello nie jest zdefiniowany. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD, a serwer kontrolera domeny hello, lub na problem w konfiguracji Data i godzina na obu komputerach. Kontroler domeny Hello odrzucone hello biletu Kerberos utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza hello są poprawnie skonfigurowane, szczególnie hello SPN konfiguracji. Upewnij się, że hello Azure AD jest przyłączony do domeny toohello tej samej domeny, jak hello tooensure kontrolera domeny, który hello kontrolera domeny ustanawia relację zaufania z usługą Azure AD. Upewnij się, Data i godzina konfiguracji hello na powitania usługi Azure AD i kontroler domeny hello są synchronizowane. |
| 13022 — usługi azure AD nie można uwierzytelnić użytkownika hello, ponieważ powitania serwera wewnętrznej bazy danych odpowiada tooKerberos prób uwierzytelnienia z powodu błędu HTTP 401. | To zdarzenie może wskazywać niepoprawną konfiguracją między usługą Azure AD i hello wewnętrznej bazy danych serwera aplikacji lub na problem w konfiguracji Data i godzina na obu komputerach. powitania serwera wewnętrznej bazy danych odrzucił bilet Kerberos hello utworzone przez usługę Azure AD. Sprawdź, że usługi Azure AD i serwer aplikacji zaplecza hello są skonfigurowane poprawnie. Upewnij się, konfiguracja Data i godzina hello na powitania usługi Azure AD i serwer aplikacji zaplecza hello są synchronizowane. |

## <a name="end-user-errors"></a>Błędy użytkownika końcowego

Ta lista zawiera błędy, które użytkownicy końcowi mogą występować w przypadku spróbuj aplikacji hello tooaccess i zakończyć się niepowodzeniem. 

| Błąd | Zalecane czynności |
| ----- | ----------------- |
| Witaj witryny sieci Web nie można wyświetlić strony hello. | Błąd ten może wystąpić użytkownika, podczas próby aplikacja hello tooaccess opublikowana, gdy aplikacja hello jest aplikacja IWA. Witaj zdefiniowane nazwy SPN dla tej aplikacji może być nieprawidłowa. W przypadku aplikacji IWA upewnij się, że tego hello SPN skonfigurowane dla tej aplikacji jest prawidłowa. |
| Witaj witryny sieci Web nie można wyświetlić strony hello. | Błąd ten może wystąpić użytkownika, podczas próby aplikacja hello tooaccess opublikowana, gdy aplikacja hello jest aplikacja usługi OWA. Może to być spowodowane jedną z następujących hello:<br><li>Hello zdefiniowane nazwy SPN dla tej aplikacji jest nieprawidłowa. Upewnij się, że ten hello SPN skonfigurowane dla tej aplikacji jest prawidłowa.</li><li>Użytkownik Hello, kto to był aplikacji hello tooaccess korzysta z konta Microsoft, zamiast hello toosign prawidłowego konta firmowego w lub hello użytkownika jest użytkownika gościa. Upewnij się, że hello użytkownik loguje się przy użyciu ich konta firmowego, że dopasowań hello domeny hello opublikowana aplikacja. Użytkownicy Account firmy Microsoft, jak i gościa nie może uzyskiwać dostęp do aplikacji IWA.</li><li>dla tej aplikacji po stronie lokalnego hello Hello użytkownik podjął próbę aplikacji hello tooaccess nie jest poprawnie zdefiniowany. Upewnij się, czy ten użytkownik ma właściwe uprawnienia hello, zgodnie z definicją dla tej aplikacji zaplecza na maszynie lokalnej hello. |
| Nie można uzyskać dostępu do tej aplikacji firmowych. Możesz są nie Autoryzowano tooaccess tej aplikacji. Autoryzacja nie powiodła się. Upewnij się, że użytkownik hello tooassign z aplikacją toothis dostępu. | Błąd ten może wystąpić użytkowników, podczas próby aplikacja hello tooaccess opublikowane użycie kont Microsoft zamiast ich toosign konto firmowe w. Błąd ten może również wystąpić gości. Użytkownicy Account firmy Microsoft i gości nie może uzyskiwać dostęp do aplikacji IWA. Upewnij się, że hello użytkownik loguje się przy użyciu ich konta firmowego, że dopasowań hello domeny hello opublikowana aplikacja.<br><br>Może nie przypisano hello użytkownika dla tej aplikacji. Przejdź toohello **aplikacji** kartę, a następnie w obszarze **użytkowników i grup**, przypisz tego użytkownika lub aplikacji toothis grupy użytkownika. |
| Ta aplikacja firmy nie jest dostępny w tej chwili. Spróbuj ponownie później... łącznika hello upłynął limit czasu. | Błąd ten może wystąpić użytkowników, podczas próby aplikacja hello tooaccess opublikowane, jeśli ich nie zostały poprawnie zdefiniowane dla tej aplikacji hello lokalnej strony. Upewnij się, czy użytkownicy mają odpowiednie uprawnienia hello zdefiniowaną dla tej aplikacji zaplecza na maszynie lokalnej hello. |
| Nie można uzyskać dostępu do tej aplikacji firmowych. Możesz są nie Autoryzowano tooaccess tej aplikacji. Autoryzacja nie powiodła się. Upewnij się, że użytkownik hello ma licencję dla usługi Azure Active Directory — wersja Premium lub Basic. | Błąd ten może wystąpić użytkowników, podczas próby tooaccess hello aplikacji, która została opublikowana, jeśli nie zostały one jawnie przypisane z licencją podstawową/Premium przez administratora hello subskrybenta. Przejdź do usługi Active Directory subskrybenta toohello **licencji** karcie i upewnij się, że ten użytkownik lub grupa użytkowników ma przypisanej licencji wersji Premium lub podstawowa. |

## <a name="my-error-wasnt-listed-here"></a>Mój błąd nie zostało przedstawione w tym miejscu

Jeśli wystąpi błąd lub problem z aplikacji serwera Proxy Azure AD, która nie ma na liście w tym przewodniku rozwiązywania problemów, chcielibyśmy toohear informacji na ten temat. Wyślij wiadomość e-mail tooour [zespołu opinii](mailto:aadapfeedback@microsoft.com) z hello szczegóły błędu hello pojawił się.

## <a name="see-also"></a>Zobacz też
* [Włącz serwer Proxy aplikacji usługi Azure Active Directory](active-directory-application-proxy-enable.md)
* [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-publish.md)
* [Włącz rejestrację jednokrotną](active-directory-application-proxy-sso-using-kcd.md)
* [Włączanie dostępu warunkowego](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
