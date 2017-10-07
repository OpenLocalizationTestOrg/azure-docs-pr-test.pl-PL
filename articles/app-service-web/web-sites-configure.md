---
title: "aaaConfigure aplikacji sieci web w usłudze aplikacji Azure"
description: "Jak tooconfigure aplikacji sieci web w usłudze Azure App Services"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Konfigurowanie aplikacji sieci Web w usłudze Azure App Service
W tym temacie wyjaśniono, jak hello tooconfigure aplikacji sieci web przy użyciu [Azure Portal].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Ustawienia aplikacji
1. W hello [Azure Portal], otwórz blok powitania dla aplikacji sieci web hello.
2. Kliknij przycisk **wszystkie ustawienia**.
3. Kliknij przycisk **ustawienia aplikacji**.

![Ustawienia aplikacji][configure01]

Witaj **ustawienia aplikacji** bloku ma ustawienia pogrupowane w różne kategorie.

### <a name="general-settings"></a>Ustawienia ogólne
**Framework w wersji**. Ustaw tych opcji, jeśli aplikacja używa tych platform: 

* **.NET framework**: hello zestawu .NET framework w wersji. 
* **PHP**: Ustaw wersję PHP hello, lub **OFF** toodisable PHP. 
* **Java**: hello wybierz wersję Java lub **OFF** toodisable Java. Hello użyj **kontener sieci Web** toochoose opcji między Tomcat i Jetty wersji.
* **Python**: Wybierz hello wersji języka Python, lub **OFF** toodisable języka Python.

Przyczyn technicznych Java, włączanie aplikacji wyłącza hello opcje .NET, PHP i Python.

<a name="platform"></a>
**Platforma**. Wybiera, czy aplikacja sieci web jest uruchamiana w środowisku 32-bitowy lub 64-bitowych. Witaj 64-bitowego środowiska wymaga trybu Basic lub Standard. Zwolnij i tryby udostępnione są zawsze uruchamiane w środowisku 32-bitowym.

**Sieci Web Sockets**. Ustaw **ON** tooenable hello protokół WebSocket; na przykład, jeśli aplikacja sieci web używa [ASP.NET SignalR] lub [użyciu biblioteki socket.io].

<a name="alwayson"></a>
**Zawsze włączone**. Domyślnie aplikacje sieci web są usuwane, jeśli są one bezczynności przez niektóre czas. Dzięki temu system hello zaoszczędzenia zasobów. W trybie Basic lub Standard, aby umożliwić **zawsze na** aplikacji hello tookeep załadować cały czas hello. Jeśli aplikacja będzie działać ciągłe zadania Webjob lub uruchamia zadania Webjob wyzwolone przy użyciu wyrażenia CRON, należy włączyć **zawsze na**, lub hello zadania sieci web mogą nie działać prawidłowo.

**Zarządzane wersji potoku**. Ustawia hello IIS [tryb potokowy]. Pozostaw ustawić tooIntegrated (domyślnie: hello), chyba że masz starszej wersji aplikacji, która wymaga starszej wersji programu IIS.

**Automatycznie wymiany**. Po włączeniu automatycznej wymiany dla miejsca wdrożenia usługi App Service automatycznie wymiany hello aplikacji sieci web w środowisku produkcyjnym po naciśnięciu gnieździe toothat aktualizacji. Aby uzyskać więcej informacji, zobacz [wdrażanie toostaging miejsc aplikacji sieci web w usłudze Azure App Service](web-sites-staged-publishing.md).

### <a name="debugging"></a>Debugowanie
**Debugowanie zdalne**. Umożliwia zdalne debugowanie. Po włączeniu umożliwia hello zdalnego debugera w Visual Studio tooconnect bezpośrednio aplikacji sieci web tooyour. Debugowanie zdalne pozostanie włączony 48 godzin. 

### <a name="app-settings"></a>Ustawienia aplikacji
Ta sekcja zawiera pary nazwa/wartość, które sieci web aplikacji zostanie załadowany po uruchomieniu. 

* W przypadku aplikacji .NET, te ustawienia są wstrzykiwane do konfiguracji .NET `AppSettings` w czasie wykonywania, zastępowanie istniejących ustawień. 
* Aplikacje PHP, Python, Java i węzła mają dostęp do tych ustawień jako zmienne środowiskowe w czasie wykonywania. Dla każdego ustawienia aplikacji są tworzone dwie zmienne środowiskowe; jeden z nazwą hello określoną przez wpis ustawienie aplikacji hello, a druga z prefiksem APPSETTING_. Zawierają hello tę samą wartość.

### <a name="connection-strings"></a>Parametry połączeń
Parametry połączenia dla połączonych zasobów. 

W przypadku aplikacji .NET, te parametry połączenia są wstrzykiwane do konfiguracji .NET `connectionStrings` ustawienia w czasie wykonywania, zastępowanie istniejących wpisów, gdzie jest klucz hello hello nazwy połączonej bazy danych. 

W przypadku aplikacji PHP, Python, Java i węzła te ustawienia będą dostępne jako zmienne środowiskowe w czasie wykonywania, prefiksem hello typu połączenia. prefiksy zmiennej środowiskowej Hello są następujące: 

* Program SQL Server:`SQLCONNSTR_`
* MySQL:`MYSQLCONNSTR_`
* Baza danych SQL:`SQLAZURECONNSTR_`
* Niestandardowe:`CUSTOMCONNSTR_`

Na przykład, jeśli parametry połączenia MySql nazwany `connectionstring1`, czy dostęp do niej za pomocą zmiennej środowiskowej hello `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Dokumenty domyślne
dokument domyślny Hello to strona sieci web hello jest wyświetlany na powitania głównego adresu URL witryny sieci Web.  Witaj pierwszy zgodnego pliku na liście hello jest używany. 

Aplikacje sieci Web może używać modułów, że trasy na podstawie adresu URL, a nie obsługujących zawartość statyczną, w którym to przypadku nie jest dokument domyślny, w związku.    

### <a name="handler-mappings"></a>Mapowania programu obsługi
Użyj tego obszaru tooadd skryptu niestandardowego procesory toohandle żądania dla określonych rozszerzeń plików. 

* **Rozszerzenie**. toobe rozszerzenie pliku Hello obsłużone, takich jak *.php lub handler.fcgi. 
* **Ścieżka do procesora skryptów**. Ścieżka bezwzględna Hello hello procesora skryptów. Toofiles żądania, odpowiadających hello rozszerzenie zostanie przetworzony przez hello procesora skryptów. Użyj ścieżki hello `D:\home\site\wwwroot` katalog główny aplikacji tooyour toorefer.
* **Dodatkowe argumenty**. Opcjonalne argumenty wiersza polecenia do procesora skryptów hello 

### <a name="virtual-applications-and-directories"></a>Wirtualne aplikacje i katalogi
aplikacje wirtualne tooconfigure i katalogi, określ poszczególne katalogi wirtualne i odpowiednie głównym witryny sieci Web toohello względną ścieżkę fizyczną. Opcjonalnie można wybrać hello **aplikacji** toomark wyboru katalogu wirtualnego jako aplikacji.

## <a name="enabling-diagnostic-logs"></a>Włączanie dzienników diagnostycznych
dzienniki diagnostyczne tooenable:

1. W bloku hello aplikacji sieci web, kliknij przycisk **wszystkie ustawienia**.
2. Kliknij przycisk **dzienniki diagnostyczne**. 

Opcje zapisywania dzienników diagnostycznych z aplikacji sieci web, która obsługuje rejestrowanie: 

* **Rejestrowanie aplikacji**. Zapisuje Dzienniki aplikacji toohello systemu plików. Rejestrowanie okresu w okresie 12 godzin. 

**Poziom**. Po włączeniu rejestrowania aplikacji, ta opcja określa hello ilość informacji, która zostanie zarejestrowane (błąd, ostrzeżenie, informacje lub pełne).

**Rejestrowanie pracy serwera sieci Web**. Dzienniki są zapisywane w hello rozszerzonym formacie W3C dziennika pliku. 

**Szczegółowe komunikaty o błędach**. Zapisuje szczegółowe informacje o błędzie komunikatów pliki htm. Witaj pliki są zapisywane w obszarze /LogFiles/DetailedErrors. 

**Śledzenie nieudanych żądań**. Żądania tooXML pliki dzienników, nie powiodło się. Witaj pliki są zapisywane w obszarze/LogFiles/W3SVC*xxx*, gdzie xxx jest unikatowy identyfikator. Ten folder zawiera plik XSL i co najmniej jeden plik XML. Czy toodownload hello pliku XSL, należy wprowadzić, ponieważ zawiera funkcję, formatowanie i filtrowania hello zawartość plików XML hello.

pliki dziennika hello tooview, należy utworzyć poświadczenia FTP w następujący sposób:

1. W bloku hello aplikacji sieci web, kliknij przycisk **wszystkie ustawienia**.
2. Kliknij przycisk **poświadczenia wdrażania**.
3. Wprowadź nazwę użytkownika i hasło.
4. Kliknij pozycję **Zapisz**.

![Konfigurowanie poświadczeń wdrożenia][configure03]

Pełna nazwa użytkownika FTP Hello jest "app\username" gdzie *aplikacji* jest nazwą hello aplikacji sieci web. Witaj nazwy użytkownika znajduje się w bloku aplikacja sieci web hello, w obszarze **Essentials**.  

![Poświadczenia wdrożenia FTP][configure02]

## <a name="other-configuration-tasks"></a>Inne zadania konfiguracji
### <a name="ssl"></a>PROTOKÓŁ SSL
W trybie Basic lub Standard możesz przekazać certyfikatów SSL dla domeny niestandardowej. Aby uzyskać więcej informacji zobacz [Włącz protokół HTTPS dla aplikacji sieci web]. 

tooview przekazane certyfikaty, kliknij przycisk **wszystkie ustawienia** > **domen niestandardowych i SSL**.

### <a name="domain-names"></a>Nazwy domen
Dodawanie niestandardowych nazw domen dla aplikacji sieci web. Aby uzyskać więcej informacji zobacz [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service].

kliknij nazwy domeny tooview **wszystkie ustawienia** > **domen niestandardowych i SSL**.

### <a name="deployments"></a>Wdrożenia
* Konfigurowanie ciągłego wdrażania. Zobacz [toodeploy przy użyciu narzędzia Git aplikacji sieci Web w usłudze Azure App Service](web-sites-deploy.md).
* Miejsc wdrożenia. Zobacz [wdrażania środowisk tooStaging dla aplikacji sieci Web w usłudze Azure App Service].

tooview Twojego miejsca wdrożenia, kliknij przycisk **wszystkie ustawienia** > **miejsc wdrożenia**.

### <a name="monitoring"></a>Monitorowanie
W trybie Basic lub Standard można sprawdzić dostępności hello punktów końcowych HTTP lub HTTPS, z zapasowej toothree rozproszona geograficznie lokalizacje. Test monitorowania kończy się niepowodzeniem, jeśli hello kod odpowiedzi HTTP jest błąd (4xx lub 5xx) lub odpowiedź hello trwa dłużej niż 30 sekund. Punkt końcowy jest traktowane jako dostępne w przypadku powodzenia testów monitorowania hello ze wszystkich hello określonej lokalizacji. 

Aby uzyskać więcej informacji, zobacz [porady: monitorować stan punktu końcowego sieci web].

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service], gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]
* [Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]
* [Skalowanie aplikacji sieci web w usłudze Azure App Service]
* [Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[wdrażania środowisk tooStaging dla aplikacji sieci Web w usłudze Azure App Service]: ./web-sites-staged-publishing.md
[Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]: ./app-service-web-tutorial-custom-ssl.md
[porady: monitorować stan punktu końcowego sieci web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]: ./web-sites-monitor.md
[tryb potokowy]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Skalowanie aplikacji sieci web w usłudze Azure App Service]: ./web-sites-scale.md
[użyciu biblioteki socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[Wypróbuj usługę App Service]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
