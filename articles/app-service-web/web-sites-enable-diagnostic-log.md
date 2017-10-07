---
title: "aaaEnable rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service"
description: "Dowiedz się, jak rejestrowania diagnostycznego tooenable i dodaj aplikację tooyour instrumentacji, a także jak tooaccess hello zarejestrowane przez usługę Azure informacje."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze aplikacji Azure
## <a name="overview"></a>Omówienie
Platforma Azure oferuje wbudowane narzędzia diagnostyczne tooassist z debugowaniem [aplikacji sieci web usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). W tym artykule omówiono sposób rejestrowania diagnostycznego tooenable i dodaj aplikację tooyour instrumentacji, a także jak tooaccess hello zarejestrowane przez usługę Azure informacje.

W tym artykule wykorzystano hello [Azure Portal](https://portal.azure.com), programu Azure PowerShell i hello toowork interfejsu wiersza polecenia platformy Azure (Azure CLI) z dzienników diagnostycznych. Aby uzyskać informacje na temat pracy z dzienników diagnostycznych przy użyciu programu Visual Studio, zobacz [Rozwiązywanie problemów z platformy Azure w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Diagnostyka serwera sieci Web i diagnostyki aplikacji
Aplikacje sieci web usługi aplikacji — Podaj funkcja diagnostyki dla rejestrowanie informacji z serwera sieci web hello i hello aplikacji sieci web. Są one logicznie podzielone na **sieci web diagnostyki serwera** i **programu application diagnostics**.

### <a name="web-server-diagnostics"></a>Diagnostyka serwera sieci Web
Można włączyć lub wyłączyć hello następujące rodzaje dzienników:

* **Szczegółowe rejestrowanie błędów** — szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej). To może zawierać informacje, które mogą pomóc ustalić, dlaczego serwer hello zwrócił kod błędu hello.
* **Nie powiodło się żądanie śledzenia** — szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śledzenia hello IIS składniki używane tooprocess hello żądania i czas hello w poszczególnych składników. Może to być przydatne, jeśli próbujesz tooincrease wydajności witryny lub określić, co powoduje określonych toobe błąd HTTP zwrócona.
* **Rejestrowanie serwera w sieci Web** — informacje o transakcjach HTTP przy użyciu hello [rozszerzonym formacie W3C dziennika pliku](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Jest to przydatne podczas określania ogólną metryki lokacji, takie jak hello liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.

### <a name="application-diagnostics"></a>Usługa Application diagnostics
Diagnostyki aplikacji umożliwia informacji toocapture generowanych przez aplikację sieci web. Aplikacje ASP.NET mogą używać hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) diagnostyki aplikacji toohello klasy toolog informacji logowania. Na przykład:

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

W czasie wykonywania mogą pobierać te dzienniki toohelp w rozwiązywaniu problemów. Aby uzyskać więcej informacji, zobacz [Azure Rozwiązywanie problemów aplikacji sieci web w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).

Aplikacje sieci web usługi aplikacji także rejestrować informacje na temat wdrażania podczas publikowania aplikacji sieci web tooa zawartości. Dzieje się to automatycznie i nie ma żadnych ustawień konfiguracji dla rejestrowania wdrożenia. Rejestrowanie wdrażania umożliwia toodetermine niepowodzenia wdrożenia. Na przykład jeśli używasz skryptu wdrażania niestandardowego można na przykład wdrożenia rejestrowania toodetermine, dlaczego skrypt hello kończy się niepowodzeniem.

## <a name="enablediag"></a>Jak tooenable diagnostyki
Diagnostyka tooenable w hello [Azure Portal](https://portal.azure.com), przejdź do bloku toohello dla aplikacji sieci web i kliknij przycisk **Ustawienia > dzienniki diagnostyczne**.

<!-- todo:cleanup dogfood addresses in screenshot -->
![Część dzienników](./media/web-sites-enable-diagnostic-log/logspart.png)

Po włączeniu **programu application diagnostics** także hello **poziom**. To ustawienie pozwala informacji hello toofilter przechwycone zbyt**informacyjny**, **ostrzeżenie** lub **błąd** informacji. Ustawienie zbyt**pełne** będzie rejestrować wszystkie informacje generowane przez aplikacji hello.

> [!NOTE]
> W przeciwieństwie do zmiany hello web.config plik włączania diagnostyki aplikacji lub zmienianie poziomów dzienników diagnostycznych nie jest odtwarzana domeny aplikacji hello aplikacji hello jest uruchamiany w ramach.
>
>

W hello [klasyczny portal](https://manage.windowsazure.com) aplikacji sieci Web **Konfiguruj** karcie, możesz wybrać **magazynu** lub **system plików** dla **serwera sieci web Rejestrowanie**. Wybieranie **magazynu** pozwala tooselect konta magazynu, który hello dzienniki będą zapisywane do kontenera obiektów blob. Wszystkie dzienniki dla **lokacji diagnostyki** są zapisywane tylko system plików toohello.

Witaj [klasyczny portal](https://manage.windowsazure.com) aplikacji sieci Web **Konfiguruj** karta zawiera również dodatkowe ustawienia dla programu application diagnostics:

* **System plików** -magazynów hello informacji diagnostycznych aplikacji toohello systemu plików aplikacji sieci web. Te pliki mogą być uzyskiwał FTP lub pobrane jako archiwum Zip przy użyciu hello Azure PowerShell lub interfejsu wiersza polecenia platformy Azure (Azure CLI).
* **Tabela magazynu** -magazynów hello informacje diagnostyczne aplikacji w hello określonego konta magazynu Azure i nazwę tabeli.
* **Magazyn obiektów blob** — informacje diagnostyczne aplikacji w określonym kontenerze konto magazynu Azure i obiektów blob hello hello magazynów.
* **Okres przechowywania** — domyślnie dzienniki nie są automatycznie usuwane z **magazynu obiektów blob**. Wybierz **ustawienia przechowywania** , a następnie wprowadź hello liczbę dni, dzienniki tookeep, jeśli chcesz, aby tooautomatically Usuń dzienniki.

> [!NOTE]
> Jeśli użytkownik [ponowne generowanie kluczy dostępu do konta magazynu](../storage/common/storage-create-storage-account.md), należy zresetować hello rejestrowania odpowiednich konfiguracji toouse hello zaktualizowane kluczy. toodo to:
>
> 1. W hello **Konfiguruj** Ustaw funkcji rejestrowania odpowiednich hello zbyt**poza**. Zapisz ustawienia.
> 2. Włącz ponownie blob konta magazynu toohello rejestrowania lub tabeli. Zapisz ustawienia.
>
>

Dowolną kombinację systemu plików, Magazyn tabel lub magazynie obiektów blob można włączyć na powitania sam czas i mieć osobny dziennik konfiguracje poziomu. Na przykład możesz toolog błędy i ostrzeżenia magazynu tooblob jako rozwiązanie długoterminowe rejestrowania, podczas włączania rejestrowania w systemie plików z poziomu verbose.

Podczas wszystkich trzech lokalizacji przechowywania Podaj hello informacji zarejestrowane zdarzenia **tabeli magazynu** i **magazynu obiektów blob** rejestrować dodatkowe informacje, takie jak identyfikator wystąpienia hello, identyfikator wątku i bardziej szczegółowe znacznik czasu (w formacie znaczników) niż rejestrowania za**system plików**.

> [!NOTE]
> Informacje przechowywane w **tabeli magazynu** lub **magazynu obiektów blob** można uzyskać tylko za pomocą klienta magazynu lub aplikacji, która bezpośrednio może współpracować z tych systemów pamięci masowej. Na przykład Eksploratora magazynu, które mogą być używane tooexplore tabeli lub obiektu blob magazynu zawiera programu Visual Studio 2013 i usługi HDInsight można uzyskać dostępu do danych przechowywanych w magazynie obiektów blob. Możesz także zapisać aplikację, która uzyskuje dostęp do usługi Azure Storage za pomocą jednego z hello [zestawów SDK usługi Azure](/downloads/#).
>
> [!NOTE]
> Można również włączyć diagnostyki z programu Azure PowerShell przy użyciu hello **AzureWebsite zestaw** polecenia cmdlet. Jeśli nie zainstalowano programu Azure PowerShell lub nie skonfigurowano jej toouse subskrypcji platformy Azure, zobacz [jak tooUse programu Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

## <a name="download"></a>Porady: pobieranie dzienników
System plików aplikacji sieci web toohello przechowywane informacje diagnostyczne są dostępne bezpośrednio za pomocą protokołu FTP. Można go również pobrać jako przy użyciu programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure hello archiwum Zip.

strukturą katalogów Hello hello dzienniki są przechowywane w wygląda następująco:

* **Dzienniki aplikacji** -/LogFiles/aplikacji /. Ten folder zawiera jeden lub więcej plików tekstowych, zawierający informacje o wygenerowane przez rejestrowanie aplikacji.
* **Nie powiodło się żądanie śladów** -/ LogFiles/W3SVC ### /. Ten folder zawiera plik XSL i co najmniej jeden plik XML. Upewnij się, Pobierz plik XSL hello na powitania, w tym samym katalogu co powitalne plików XML, ponieważ plik XSL hello udostępnia funkcje dotyczące formatowania i filtrowanie zawartości hello hello XML plików podczas wyświetlania w przeglądarce Internet Explorer.
* **Szczegółowe dzienniki błędów** -/LogFiles/DetailedErrors /. Ten folder zawiera jeden lub więcej plików htm, które zapewniają szczegółowe informacje, które wystąpiły błędy HTTP.
* **Dzienniki serwera w sieci Web** -/LogFiles/http/RawLogs. Ten folder zawiera jeden lub więcej plików tekst sformatowany przy użyciu hello [rozszerzonym formacie W3C dziennika pliku](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
* **Dzienniki wdrożenia** -/ LogFiles/Git. Ten folder zawiera dzienniki generowane przez procesy wewnętrznego wdrażania hello używane przez aplikacje sieci web platformy Azure, a także wdrożeń Git w dziennikach.

### <a name="ftp"></a>FTP
informacje diagnostyczne tooaccess za pomocą protokołu FTP, odwiedź stronę hello **pulpitu nawigacyjnego** aplikacji sieci web w hello [klasyczny portal](https://manage.windowsazure.com). W hello **szybkiego dostępu** Użyj hello **dzienników diagnostycznych FTP** łączenie plików dziennika hello tooaccess za pomocą protokołu FTP. Witaj **użytkowników usługi FTP/wdrożenia** wpis zawiera hello nazwę użytkownika, który ma być używane tooaccess hello FTP lokacji.

> [!NOTE]
> Jeśli hello **użytkowników usługi FTP/wdrożenia** wpis nie jest ustawiona, lub pamiętasz hasła powitania dla tego użytkownika, można utworzyć nowego użytkownika i hasło, które znajdują się za pomocą hello **resetowanie poświadczeń wdrażania** łącze w hello **szybkiego dostępu** sekcji hello **pulpitu nawigacyjnego**.
>
>

### <a name="download-with-azure-powershell"></a>Pobierz przy użyciu programu Azure PowerShell
pliki dziennika hello toodownload, uruchomić nowe wystąpienie programu Azure PowerShell i użyj hello następujące polecenie:

    Save-AzureWebSiteLog -Name webappname

Spowoduje to zapisanie hello dzienniki dla aplikacji sieci web hello określony przez hello **— nazwa** parametru tooa plik o nazwie **logs.zip** w bieżącym katalogu hello.

> [!NOTE]
> Jeśli nie zainstalowano programu Azure PowerShell lub nie skonfigurowano jej toouse subskrypcji platformy Azure, zobacz [jak tooUse programu Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="download-with-azure-command-line-interface"></a>Pobierz z interfejsu wiersza polecenia platformy Azure
pliki dziennika hello toodownload przy użyciu hello interfejsu wiersza polecenia Azure, otwórz nowy wiersz polecenia, programu PowerShell, Bash lub sesję terminala i wprowadź hello następujące polecenie:

    azure site log download webappname

Spowoduje to zapisanie dzienniki hello hello aplikacji sieci web o nazwie "webappname" tooa plik o nazwie **diagnostics.zip** w bieżącym katalogu hello.

> [!NOTE]
> Jeśli nie zainstalowano hello interfejsu wiersza polecenia platformy Azure (Azure CLI) lub nie skonfigurowano jej toouse subskrypcji platformy Azure, zobacz [jak tooUse interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).
>
>

## <a name="how-to-view-logs-in-application-insights"></a>Porady: Wyświetl dzienniki w usłudze Application Insights
Visual Studio Application Insights udostępnia narzędzia do filtrowania i wyszukiwania dzienników oraz korelowanie hello dzienniki z żądaniami oraz innymi zdarzeniami.

1. Dodaj hello zestaw SDK usługi Application Insights tooyour projektu w programie Visual Studio.
   * W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie Dodaj usługę Application Insights. Poprowadzą Cię przez kroki, które obejmują tworzenie zasobu usługi Application Insights. [Dowiedz się więcej](../application-insights/app-insights-asp-net.md)
2. Dodaj hello nasłuchującego śledzenia pakietu tooyour projektu.
   * Kliknij prawym przyciskiem myszy projekt i wybierz polecenie Zarządzaj pakietami NuGet. Wybierz `Microsoft.ApplicationInsights.TraceListener` [Dowiedz się więcej](../application-insights/app-insights-asp-net-trace-logs.md)
3. Przekaż swój projekt i uruchomić toogenerate dane dziennika.
4. W hello [Azure Portal](https://portal.azure.com/), nowy zasób usługi Application Insights tooyour Przeglądaj i Otwórz **wyszukiwania**. Zobaczysz danych dziennika, wraz z żądania, użytkowania i innych danych telemetrycznych. Niektóre dane telemetryczne może potrwać kilka minut tooarrive: kliknij przycisk Odśwież. [Dowiedz się więcej](../application-insights/app-insights-diagnostic-search.md)

[Dowiedz się więcej na temat wydajności śledzenia z usługą Application Insights](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a>Porady: strumienia dzienników
Podczas tworzenia aplikacji, często jest przydatne toosee rejestrowanie informacji w czasie niemal rzeczywistym. Można to zrobić przez przesyłania strumieniowego rejestrowanie informacji tooyour środowiska programowania przy użyciu programu Azure PowerShell lub hello interfejsu wiersza polecenia platformy Azure.

> [!NOTE]
> Niektóre typy rejestrowania buforu zapisu toohello pliku dziennika, co może skutkować zdarzenia poza kolejnością w strumieniu hello. Na przykład wpis dziennika aplikacji, która występuje, gdy użytkownik odwiedza stronę mogą być wyświetlane w strumieniu hello przed hello odpowiedni HTTP dziennika zapis hello żądania strony.
>
> [!NOTE]
> Przesyłanie strumieniowe dziennika również strumienia informacji przechowywanych w hello pliku tekstowego tooany **D:\\macierzystego\\LogFiles\\ ** folderu.
>
>

### <a name="streaming-with-azure-powershell"></a>Przesyłania strumieniowego przy użyciu programu Azure PowerShell
informacje o rejestrowaniu toostream, uruchomić nowe wystąpienie programu Azure PowerShell i użyć hello następujące polecenie:

    Get-AzureWebSiteLog -Name webappname -Tail

Spowoduje to połączenie toohello aplikacji sieci web określonej przez hello **— nazwa** parametru i rozpocząć przesyłanie strumieniowe okno programu PowerShell toohello informacje, jak zdarzenia dziennika są dokonywane na powitania aplikacji sieci web. Wszystkie informacje zapisane toofiles kończące się txt, log lub htm, które są przechowywane w katalogu /LogFiles hello (d: lub głównej/pliki dziennika) zostanie przesłany strumieniowo toohello konsoli lokalnej.

toofilter określonych zdarzeń, takich jak błędy, użyj hello **-komunikat** parametru. Na przykład:

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

typy określonego dziennika toofilter, takich jak HTTP, użyj hello **-ścieżka** parametru. Na przykład:

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

Lista dostępnych ścieżek, użyj parametru - ListPath hello toosee.

> [!NOTE]
> Jeśli nie zainstalowano programu Azure PowerShell lub nie skonfigurowano jej toouse subskrypcji platformy Azure, zobacz [jak tooUse programu Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).
>
>

### <a name="streaming-with-azure-command-line-interface"></a>Przesyłanie strumieniowe z interfejsu wiersza polecenia platformy Azure
informacje o rejestrowaniu toostream, otwórz nowy wiersz polecenia, programu PowerShell, Bash lub sesję terminala i wprowadź hello następujące polecenie:

    azure site log tail webappname

Spowoduje to łączenie toohello aplikacji sieci web o nazwie "webappname" i rozpocząć przesyłanie strumieniowe okna toohello informacje, jak zdarzenia dziennika są dokonywane na powitania aplikacji sieci web. Wszystkie informacje zapisane toofiles kończące się txt, log lub htm, które są przechowywane w katalogu /LogFiles hello (d: lub głównej/pliki dziennika) zostanie przesłany strumieniowo toohello konsoli lokalnej.

toofilter określonych zdarzeń, takich jak błędy, użyj hello **— filtr** parametru. Na przykład:

    azure site log tail webappname --filter Error

typy określonego dziennika toofilter, takich jak HTTP, użyj hello **— ścieżka** parametru. Na przykład:

    azure site log tail webappname --path http

> [!NOTE]
> Jeśli nie zainstalowano hello interfejsu wiersza polecenia platformy Azure lub nie skonfigurowano jej toouse subskrypcji platformy Azure, zobacz [jak tooUse interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).
>
>

## <a name="understandlogs"></a>Porady: zrozumienie dzienników diagnostycznych
### <a name="application-diagnostics-logs"></a>Dzienniki diagnostyki aplikacji
Diagnostyka aplikacji są przechowywane informacje w określonym formacie aplikacji .NET, w zależności od tego, czy system plików toohello dzienników, Magazyn tabel do przechowywania lub magazynu obiektów blob. zestaw podstawowy Hello danych przechowywanych jest hello sama we wszystkich trzech typów magazynu - wystąpiło zdarzenie hello hello datę i godzinę, identyfikator procesu hello wytworzonego hello zdarzeń, typ zdarzenia hello (informacje, ostrzeżenie, błąd) i wiadomości powitania zdarzeń.

**System plików**

Każdy wiersz zarejestrowane toohello system plików lub odbierane przy użyciu przesyłania strumieniowego będą hello następującego formatu:

    {Date}  PID[{process id}] {event type/level} {message}

Na przykład zdarzenie błędu pojawiały się podobne toohello następujące czynności:

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

Rejestrowanie toohello systemu plików informacje hello najprostszych metod hello trzy dostępne, tylko czas hello, identyfikator procesu, poziom zdarzenia i wiadomości.

**Table Storage**

Po zalogowaniu się tootable magazynu, dodatkowe właściwości są używane toofacilitate wyszukiwanie hello danymi przechowywanymi w tabeli hello, a także bardziej szczegółowe informacje w zdarzeniu hello. Witaj następujących właściwości (kolumny) są używane dla każdej jednostki (wiersz) przechowywane w tabeli hello.

| Nazwa właściwości | Format wartości / |
| --- | --- |
| PartitionKey |Data/Godzina hello zdarzenia w formacie yyyyMMddHH |
| RowKey |Wartość identyfikatora GUID, który unikatowo identyfikuje tę jednostkę |
| Znacznik czasu |Wystąpił Hello Data i godzina hello zdarzeń |
| EventTickCount |Witaj Data i godzina hello zdarzeń wystąpił w formacie znaczników (większą dokładność) |
| ApplicationName |Nazwa aplikacji sieci web Hello |
| Poziom |Poziom zdarzenia (np. błąd, ostrzeżenie, informacje) |
| Identyfikator zdarzenia |Identyfikator zdarzenia Hello tego zdarzenia<p><p>Jeśli nie została określona, domyślnie przyjmowana too0 |
| Identyfikator wystąpienia |Wystąpienie hello aplikacji sieci web, która nawet hello wystąpił w |
| Identyfikator procesu |Identyfikator procesu |
| TID |Identyfikator wątku Hello wątku hello, wytworzonego hello zdarzeń |
| Komunikat |Szczegóły komunikatu o zdarzeniu |

**Blob Storage**

Po zalogowaniu się tooblob magazynu, dane są przechowywane w formacie wartości rozdzielanych przecinkami (CSV). Podobne tootable magazynu, dodatkowe pola są rejestrowane tooprovide bardziej szczegółowe informacje o zdarzeniu hello. Witaj następujące właściwości są używane dla każdego wiersza w hello CSV:

| Nazwa właściwości | Format wartości / |
| --- | --- |
| Date |Wystąpił Hello Data i godzina hello zdarzeń |
| Poziom |Poziom zdarzenia (np. błąd, ostrzeżenie, informacje) |
| ApplicationName |Nazwa aplikacji sieci web Hello |
| Identyfikator wystąpienia |Wystąpienie hello aplikacji sieci web, którą hello zdarzeń wystąpił w |
| EventTickCount |Witaj Data i godzina hello zdarzeń wystąpił w formacie znaczników (większą dokładność) |
| Identyfikator zdarzenia |Identyfikator zdarzenia Hello tego zdarzenia<p><p>Jeśli nie została określona, domyślnie przyjmowana too0 |
| Identyfikator procesu |Identyfikator procesu |
| TID |Identyfikator wątku Hello wątku hello, wytworzonego hello zdarzeń |
| Komunikat |Szczegóły komunikatu o zdarzeniu |

Hello dane przechowywane w obiekcie blob będzie wyglądać podobnie toohello następujące:

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> pierwszy wiersz Hello hello dziennika będzie zawierać nagłówki kolumn hello reprezentowany w tym przykładzie.
>
>

### <a name="failed-request-traces"></a>Nie powiodło się żądanie śledzenia
Dane śledzenia nieudanych żądań, są przechowywane w plikach XML o nazwie **fr ### .xml**. toomake go łatwiejsze tooview hello rejestrowane informacje, arkusz stylów XSL o nazwie **freb.xsl** znajduje się w hello sam katalog hello plików XML. Otwarcie jednej z plikami XML hello w programie Internet Explorer będzie używać tooprovide arkusza stylów XSL hello sformatowany wyświetlanie informacji o śledzeniu hello. Będzie ona widoczna podobne toohello następujące czynności:

![w przeglądarce hello żądań zakończonych niepowodzeniem](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>Szczegółowe dzienniki błędów
Szczegółowe dzienniki błędów są dokumentów HTML, które zapewniają bardziej szczegółowe informacje o błędach HTTP, które wystąpiły. Ponieważ są one po prostu dokumentów HTML, ich można wyświetlić w przeglądarce sieci web.

### <a name="web-server-logs"></a>Dzienniki serwera sieci Web
Witaj dzienniki serwera sieci web są sformatowane przy użyciu hello [rozszerzonym formacie W3C dziennika pliku](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx). Te informacje mogą być odczytywane za pomocą edytora tekstu lub analizować przy użyciu narzędzia, takie jak [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).

> [!NOTE]
> Witaj dzienniki generowane przez aplikacje sieci web Azure nie obsługują hello **s-computername**, **s-ip**, lub **cs-version** pola.
>
>

## <a name="nextsteps"></a> Następne kroki
* [Jak tooMonitor aplikacji sieci Web](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [Rozwiązywanie problemów aplikacji sieci web platformy Azure w programie Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md)
* [Analizowanie dzienników aplikacji sieci web w usłudze HDInsight](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
>
>

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
* Toohello przewodnik zmiany hello starego portalu toohello nowego portalu dla: [odwołanie do nawigowania hello portalu Azure](http://go.microsoft.com/fwlink/?LinkId=529715)
