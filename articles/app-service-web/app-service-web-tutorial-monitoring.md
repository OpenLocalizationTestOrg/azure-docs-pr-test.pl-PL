---
title: aaaMonitor aplikacji sieci Web | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się monitorowania na aplikację sieci Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Monitor usługi aplikacji
W tym samouczku przedstawiono sposób monitorowania aplikacji i przy użyciu hello platformy wbudowane narzędzia toosolve problemów, jeśli występują.

Każdej sekcji tego dokumentu przechodzi przez określoną funkcję. Korzystanie z funkcji hello razem umożliwiają:
- Identyfikowanie problemu w aplikacji.
- Określanie, kiedy hello przyczyną problemu jest kod lub hello platformy.
- Zawęź hello źródłem problemu hello w kodzie.
- Debugowanie i rozwiązywania problemu hello.

## <a name="before-you-begin"></a>Przed rozpoczęciem
- Należy toomonitor aplikacji sieci Web i wykonaj hello opisane kroki.
    - Można utworzyć aplikacji hello wykonaj czynności opisane w hello [tworzenie aplikacji ASP.NET na platformie Azure z bazy danych SQL](app-service-web-tutorial-dotnet-sqldatabase.md) samouczka.

- Jeśli chcesz tootry **zdalnego debugowania** aplikacji, potrzebujesz programu Visual Studio.
    - Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello wolnego [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.

## <a name="metrics"></a>Krok 1 — widok metryk
**Metryki** są przydatne toounderstand:
- Kondycja aplikacji
- Wydajność aplikacji
- Użycie zasobów

Po zbadaniu problemu z aplikacją, przeglądanie metryki jest toostart dobrym miejscem. Azure portal ma toovisually szybko sprawdzić za pomocą aplikacji hello metryki **Azure Monitor**.

Metryki udostępnianie widok historycznych w kilku agregacjach klucza dla aplikacji. Dla dowolnej aplikacji hostowanej w usłudze app service należy monitorować zarówno hello aplikacji sieci Web, jak i hello planu usługi aplikacji.

> [!NOTE]
> Plan usługi aplikacji reprezentuje kolekcję hello toohost fizyczne zasoby używane aplikacje. Wszystkie aplikacje przypisane tooan planu usługi aplikacji udziału hello zasobów zdefiniowana przez nią stosowanie koszt toosave odnośnie do hostowania wielu aplikacji.
>
> Plany usługi App Service definiują następujące elementy:
> * Region: Europa Północna, wschodnie stany USA, Azja południowo-wschodnia,... itd.
> * Rozmiar wystąpienia: Mały, Średni, duża itp.
> * Liczba skali: jedną, dwie lub trzy wystąpienia, itp.
> * Jednostka SKU: Wolne Shared Basic, Standard, Premium, itp.

metryki tooreview dla aplikacji sieci Web, przejdź toohello **omówienie** bloku aplikacji hello ma toomonitor. W tym miejscu można wyświetlić wykresu dla metryki aplikacji jako **Kafelek monitorowanie**. Kliknij przycisk tooedit kafelka hello i skonfiguruj jakie tooview metryki oraz hello toodisplay zakresu czasu.

W bloku zasobów hello domyślne udostępnia widok hello żądań aplikacji i błędów dotyczących hello ostatniej godziny.
![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Jak widać w przykładzie hello mamy aplikacji, która generuje wiele **błędy serwera HTTP**. duża liczba błędów Hello jest hello pierwsze wskazanie potrzebne tooinvestigate tej aplikacji.

> [!TIP]
> Więcej informacji na temat Monitora Azure z hello następującego łącza:
> - [Rozpoczynanie pracy z monitorem Azure](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Metryki Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Obsługiwane metryki z monitorem Azure](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure pulpity nawigacyjne](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Krok 2 — Konfigurowanie alertów
**Alerty** może być skonfigurowany tootrigger przy użyciu określonych warunków dla aplikacji.

W [krok 1 — widok metryki](#metrics), widzieliśmy, że aplikacja hello miała dużą liczbę błędów.

Pozwala skonfigurować alert tooautomatically Otrzymuj powiadomienia w przypadku błędów. W takim przypadku firma Microsoft ma hello toosend alertów i wiadomości e-mail za każdym razem, gdy hello liczbę błędów HTTP 50 X przechodzi przez określony próg.

toocreate alertu, przejdź zbyt**monitorowanie** > **alerty** i kliknij przycisk **[+] Dodaj Alert**.

![Alerty](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Podaj wartości dla konfiguracji alertu hello:
- **Zasób:** hello toomonitor lokacji hello alert.
- **Nazwa:** nazwę alertu, w tym przypadku: *wysokiej HTTP 50 X*.
- **Opis:** wyjaśnienie ten alert spojrzenie na zwykły tekst.
- **Alert dotyczący:** alerty można przeglądać metryki lub zdarzeń, w tym przykładzie czekamy na metryki.
- **Metryka:** jakie toomonitor metryki, w tym przypadku: *błędy serwera HTTP*.
- **Warunek:** po tooalert, w tym przypadku wybierz hello *większe* opcji.
- **Próg:** toolook wartości, co jest w tym przypadku: *400*.
- **Okres:** alerty działają na powitania średnia wartość metryki. Mniejsze okresów uzyskanie bardziej poufnego alerty. w takim przypadku czekamy na *5 minut*.
- **Wyślij wiadomość e-mail właściciele i Współautorzy:** w takim przypadku: *włączone*.

Teraz, gdy hello alert jest tworzony wiadomości e-mail są wysyłane za każdym razem, gdy hello aplikacja przechodzi powyżej wartości progowej hello skonfigurowane. Aktywne alerty mogą być przeglądane również na powitania portalu Azure.

![Wyzwalanie alertów](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Dowiedz się więcej o alertach Azure z hello następującego łącza:
> - [Co to są alerty na platformie Microsoft Azure](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Podejmij działanie metryk](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Tworzenie metryk alertów](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>Krok 3 — Pomocnik usługi aplikacji
**Pomocnik usługi aplikacji** oferuje toomonitor wygodny sposób aplikacji z natywnym środowiskiem urządzenia przenośnego (z systemem iOS lub Android).

Użyj Pomocnik usługi aplikacji:
- Przejrzyj metryki aplikacji
- Przejrzyj i korzystania z aplikacji, alertów i zalecenia
- Rozwiązywania problemów z podstawowego (przeglądania, uruchom, Zatrzymaj, ponowne uruchomienie aplikacji hello)
- Uzyskiwanie powiadomień wypychanych dla zdarzeń krytycznych.

![Pomocnik usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Aplikacja usługi pomocnika sklepu](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play pomocniczy usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Pomocnik usługi aplikacji można zainstalować z hello [sklepu z aplikacjami](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) lub [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>Krok 4 — diagnozowanie i rozwiązywanie problemów
**Diagnozowanie i rozwiązywanie problemów** pomaga oddzielić problemy aplikacji tworzą problemy platformy. On również sugerować możliwe ograniczenie jego skutków tooget toohealthy wstecz Twojej aplikacji sieci Web.

![Diagnozowanie i rozwiązywanie problemów](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Kontynuowaniem hello przykład formularz poprzednie kroki, zobaczysz, że aplikacja hello ma zostać problemy dostępności. Z kolei hello platformy dostępności nie zostały przeniesione od 100%.

Gdy aplikacji hello nastąpił problem i hello platformy pozostaje w górę, jest jasne wskazanie, że firma Microsoft ma do czynienia z problemu z aplikacją.

## <a name="logging"></a>Krok 5 — rejestrowanie
Teraz, gdy będziemy mieć zawęzić hello problemu z aplikacją tooan błędów, może przyjrzymy się tooget Dzienniki aplikacji i serwerze hello więcej informacji.

Rejestrowanie umożliwia toocollect zarówno **programu Application Diagnostics** i **diagnostyki serwera sieci Web** dzienników aplikacji sieci Web.

### <a name="application-diagnostics"></a>Usługa Application Diagnostics
Diagnostyki aplikacji umożliwia możesz toocapture śladów utworzonego przez aplikacji hello w czasie wykonywania.

Dodawanie tooyour śledzenie aplikacji znacznie skraca toodebug możliwości, a punkt przypięcia problemy.

W programie ASP.NET, możesz zalogować się przy użyciu śladów aplikacji [System.Diagnostics.Trace — klasa](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate zdarzenia, które są przechwytywane przez infrastrukturę dziennika hello. Można również określić ważność hello śledzenia hello łatwiejsze filtrowania.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
Rejestrowanie aplikacji tooenable Przejdź zbyt**monitorowanie** > **dzienników diagnostycznych** i włączyć rejestrowania aplikacji przy użyciu hello przełączników.

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Dzienniki aplikacji może być aplikacja sieci Web tooyour przechowywanych w systemie plików lub wypchnięty tooblob magazynu. Scenariusze produkcji jest zalecana toouse magazynu obiektów blob.

> [!IMPORTANT]
> Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji. W scenariuszach produkcji zaleca się w dzienniku błędów. Pełniejsze rejestrowanie należy włączyć tylko podczas badania problemów.

 ### <a name="web-server-diagnostics"></a>Diagnostyka serwera sieci Web
Dzienniki serwera sieci Web są generowane, nawet jeśli aplikacja nie została zinstrumentowana. Usługi aplikacji może zbierać trzy różne typy dzienników serwera:

- **Rejestrowanie pracy serwera sieci Web**
    - Informacje o transakcjach HTTP przy użyciu hello [rozszerzonym formacie W3C dziennika pliku](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Przydatne podczas określania ogólną metryki lokacji, takie jak hello liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.
- **Szczegółowe informacje o błędzie logowania**
    - Szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej).
    - [Dowiedz się więcej na temat rejestrowania szczegółowe informacje o błędzie](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Śledzenie niepomyślnych żądań**
    - Szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śledzenia hello komponenty używane tooprocess hello żądania i hello czas w poszczególnych składników.
    - Żądań zakończonych niepowodzeniem dzienniki są przydatne podczas próby tooisolate, co jest przyczyną błędu HTTP.
    - [Dowiedz się więcej na temat śledzenia nieudanych żądań](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

Rejestrowanie serwera tooenable:
- Przejdź za**monitorowanie** > **dzienników diagnostycznych**.
- Włącz hello różne rodzaje diagnostyki serwera sieci Web za pomocą przełączników hello.

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji. W przypadku scenariuszy produkcji dzienniki błędów są zalecane, włączyć tylko pełniejsze rejestrowanie podczas badania problemów.

### <a name="accessing-logs"></a>Uzyskiwanie dostępu do dzienników
Dzienników przechowywanych w magazynie obiektów blob są dostępne za pomocą Eksploratora usługi Storage platformy Azure. Dzienników przechowywanych w aplikacji sieci Web hello systemu plików są dostępne za pośrednictwem FTP w obszarze hello następującej ścieżki:

- **Dzienniki aplikacji** - `%HOME%/LogFiles/Application/`.
    - Ten folder zawiera jeden lub więcej plików tekstowych, zawierający informacje o wygenerowane przez rejestrowanie aplikacji.
- **Nie powiodło się żądanie śladów** - `%HOME%/LogFiles/W3SVC#########/`.
    - Ten folder zawiera plik XSL i co najmniej jeden plik XML.
- **Szczegółowe dzienniki błędów** - `%HOME%/LogFiles/DetailedErrors/`.
    - Ten folder zawiera co najmniej jeden plik .htm o wiele informacji dotyczących błędów HTTP wygenerowany przez aplikację.
- **Dzienniki serwera w sieci Web** - `%HOME%/LogFiles/http/RawLogs`.
    - Ten folder zawiera jeden lub więcej plików tekst sformatowany przy użyciu hello W3C rozszerzony format pliku dziennika.

## <a name="streaming"></a>Krok 6 - dzienników przesyłania strumieniowego
Dzienniki przesyłania strumieniowego są wygodne podczas debugowania aplikacji, ponieważ zaoszczędzić czas, w porównaniu zbyt[podczas uzyskiwania dostępu do dzienników hello](#Accessing-Logs) za pośrednictwem FTP.

Usługi aplikacji może być przesyłany strumieniowo **Dzienniki aplikacji** i **dzienniki serwera sieci Web** zgodnie z ich wygenerowaniu.

> [!TIP]
> Przed podjęciem próby toostream dzienniki, upewnij się, że włączono zbieranie dzienników zgodnie z opisem w hello [rejestrowanie](#logging) sekcji.

Dzienniki toostream Przejdź zbyt**monitorowanie**> **strumienia dziennika**. Wybierz **Dzienniki aplikacji** lub **dzienniki serwera w sieci Web** zależności informacjach szukasz. W tym miejscu mogą również wstrzymać, uruchom ponownie i hello buforu.

![Dzienniki przesyłania strumieniowego](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Dzienniki są generowane tylko, gdy ruchu w aplikacji hello, a także może zwiększyć poziom szczegółowości hello tooget dzienniki więcej zdarzeń lub informacji.

## <a name="remote"></a>Krok 7. debugowanie zdalne
Po utworzeniu wskazywanej przez kod pin hello źródło problemów aplikacji hello użyj **zdalnego debugowania** toowalk za pośrednictwem hello kodu.

Zdalne debugowanie umożliwia, możesz dołączyć debuger tooyour aplikacji sieci Web w chmurze hello. Można ustawić punktów przerwania, manipulowanie nimi pamięci bezpośrednio, krokowo kodu oraz nawet zmienić ścieżkę kodu hello, podobnie jak w przypadku aplikacji uruchomionej na komputerze lokalnym.

tooattach hello debugera tooyour aplikacji uruchomionej w chmurze hello:

- Za pomocą programu Visual Studio 2017 r hello Otwórz rozwiązanie dla aplikacji hello ma toodebug
- Ustaw niektórych punktach hamulca, tak jak dla rozwoju lokalnych.
- Otwórz **Eksplorator chmury** (kont. + /, ctrl + x).
- Zaloguj się przy użyciu poświadczeń platformy azure, zgodnie z potrzebami.
- Znajdź aplikacji hello ma toodebug
- Wybierz **dołączyć debuger** hello formularza **akcje** okienka.

![Debugowanie zdalne](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio konfiguruje aplikację do zdalnego debugowania i uruchamia okno przeglądarki, który nawiguje tooyour aplikacji. Przejrzyj punkty przerwania tootrigger aplikacji i wykonywać krokowo kodu hello.

> [!WARNING]
> Nie zaleca się uruchamiania w trybie debugowania w środowisku produkcyjnym. Jeśli wystąpienia serwera toomultiple nie skalowania aplikacji produkcyjnych, debugowanie zapobiec powitania serwera sieci web z odpowiada tooother żądań. Podczas rozwiązywania problemów w środowisku produkcyjnym, najlepiej zasobu jest zbyt[skonfigurować rejestrowanie](#logging) i [usługi Application Insights](#insights).



## <a name="explorer"></a>Krok 8 - Eksploratora procesów
Gdy aplikacja jest skalowana w poziomie toomore niż jedno wystąpienie **Eksploratora procesów** mogą ułatwić identyfikację wystąpienia określonych problemów.

Użyj **przetworzyć Explorer** do:

- Wylicza wszystkie procesy hello w różnych wystąpieniach planu usługi aplikacji.
- Przechodzenie i wyświetlanie uchwytów hello i moduły skojarzone z każdym procesie.
- Liczba Procesora widoku, zestaw roboczy i wątku na powitania przetworzyć poziomu toohelp zidentyfikować wyczerpania procesów
- Znajdź dojść otwartych plików, a nawet kill wystąpienia określonego procesu.

Eksploratora procesów można znaleźć w **monitorowanie** > **Eksploratora procesów**.

![Eksplorator procesów](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Krok 9 - usługi Application Insights
**Usługa Application Insights** zapewnia profilowania aplikacji i zaawansowanych możliwości monitorowania dla aplikacji.

Użyj usługi Application Insights toodetect i diagnozowanie wyjątków i problemy z wydajnością w aplikacji sieci Web.

Można włączyć usługi Application Insights dla aplikacji sieci Web, w obszarze **monitorowanie** > **usługi Application Insights**

> [!NOTE]
> Usługa Application Insights może monitować tooinstall hello usługi Application Insights lokacji rozszerzenia toostart zbierania danych. Instalowanie rozszerzenia lokacji hello powoduje ponowne uruchomienie aplikacji.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Usługa Application Insights ma zaawansowanych funkcji ustawiona, toolearn, wykonaj łącza hello w hello [następne kroki](#next) sekcji.

## <a name="next"></a> Następne kroki

 - [Co to jest usługa Application Insights](..\application-insights\app-insights-overview.md)
 - [Monitorowanie wydajności aplikacji sieci web platformy Azure przy użyciu usługi Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Monitorowanie dostępności i szybkość reakcji każdej witrynie sieci web z usługą Application Insights](..\application-insights\app-insights-monitor-web-app-availability.md)
