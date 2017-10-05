---
title: Monitorowanie aplikacji sieci Web | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak skonfigurować monitorowanie w aplikacji sieci Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a>Monitor usługi aplikacji
W tym samouczku przedstawiono sposób monitorowania aplikacji i za pomocą narzędzi wbudowanych platformy do rozwiązywania problemów w momencie wystąpienia.

Każdej sekcji tego dokumentu przechodzi przez określoną funkcję. Przy użyciu funkcji razem umożliwiają:
- Identyfikowanie problemu w aplikacji.
- Określanie, kiedy problem spowodowany kodu lub platformy.
- Zawęź źródłem problemu w kodzie.
- Debugowanie i rozwiązywania problemu.

## <a name="before-you-begin"></a>Przed rozpoczęciem
- Należy aplikacji sieci Web w taki sposób, aby monitorować i wykonaj kroki obramowane.
    - Wykonanie kroków opisanych w aplikacji można utworzyć [tworzenie aplikacji ASP.NET na platformie Azure z bazy danych SQL](app-service-web-tutorial-dotnet-sqldatabase.md) samouczka.

- Jeśli chcesz wypróbować **zdalnego debugowania** aplikacji, potrzebujesz programu Visual Studio.
    - Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i korzystać z BEZPŁATNEJ [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).
    - Podczas instalacji programu Visual Studio upewnij się, że jest włączona opcja **Programowanie na platformie Azure**.

## <a name="metrics"></a>Krok 1 — widok metryk
**Metryki** są przydatne do zrozumienia:
- Kondycja aplikacji
- Wydajność aplikacji
- Użycie zasobów

Po zbadaniu problemu z aplikacją, przeglądanie metryki jest dobrym miejscem do rozpoczęcia. Azure portal ma szybkie wizualnie Sprawdź swoją aplikację przy użyciu metryk **Azure Monitor**.

Metryki udostępnianie widok historycznych w kilku agregacjach klucza dla aplikacji. Dla dowolnej aplikacji hostowanej w usłudze app service należy monitorować zarówno aplikacji sieci Web i plan usługi aplikacji.

> [!NOTE]
> Plan usługi App Service reprezentuje kolekcję zasobów fizycznych służących do hostowania aplikacji. Wszystkie aplikacje przypisane do planu usługi App Service współdzielą zasoby przez niego zdefiniowane, ograniczając koszt hostowania wielu aplikacji.
>
> Plany usługi App Service definiują następujące elementy:
> * Region: Europa Północna, wschodnie stany USA, Azja południowo-wschodnia,... itd.
> * Rozmiar wystąpienia: Mały, Średni, duża itp.
> * Liczba skali: jedną, dwie lub trzy wystąpienia, itp.
> * Jednostka SKU: Wolne Shared Basic, Standard, Premium, itp.

Aby przejrzeć metryki dla aplikacji sieci Web, przejdź do **omówienie** bloku aplikacji, którą chcesz monitorować. W tym miejscu można wyświetlić wykresu dla metryki aplikacji jako **Kafelek monitorowanie**. Kliknij Kafelek, aby edytowanie i konfigurowanie jakie metryk umożliwiają wyświetlenie i zakres czasu do wyświetlenia.

Domyślnie bloku zasobów zawiera widok dla żądań aplikacji i błędy w ciągu ostatniej godziny.
![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Jak widać w tym przykładzie mamy aplikacji, która generuje wiele **błędy serwera HTTP**. Duża liczba błędów jest pierwsze wskazanie potrzebne w celu zbadania tej aplikacji.

> [!TIP]
> Więcej informacji na temat Monitora Azure z następujących łączy:
> - [Rozpoczynanie pracy z monitorem Azure](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Metryki Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Obsługiwane metryki z monitorem Azure](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure pulpity nawigacyjne](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a>Krok 2 — Konfigurowanie alertów
**Alerty** można skonfigurować do wyzwalania określonych warunków dla aplikacji.

W [krok 1 — widok metryki](#metrics), widzieliśmy, że aplikacja będzie miała dużą liczbę błędów.

Umożliwia konfigurowanie alert, aby automatycznie Otrzymuj powiadomienia w przypadku błędów. W takim przypadku chcemy alert do wysyłania i wiadomości e-mail za każdym razem, gdy liczba błędów HTTP 50 X przechodzi przez określony próg.

Aby utworzyć alert, przejdź do **monitorowanie** > **alerty** i kliknij przycisk **[+] Dodaj Alert**.

![Alerty](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Podaj wartości w konfiguracji alertu:
- **Zasób:** lokacji do monitorowania z alertem.
- **Nazwa:** nazwę alertu, w tym przypadku: *wysokiej HTTP 50 X*.
- **Opis:** wyjaśnienie ten alert spojrzenie na zwykły tekst.
- **Alert dotyczący:** alerty można przeglądać metryki lub zdarzeń, w tym przykładzie czekamy na metryki.
- **Metryka:** jakie Metryka do monitorowania, w tym przypadku: *błędy serwera HTTP*.
- **Warunek:** kiedy alertu, w tym przypadku wybierz *większe* opcji.
- **Próg:** co to jest wartość do wyszukania w takim przypadku: *400*.
- **Okres:** alerty działają na średnia wartość metryki. Mniejsze okresów uzyskanie bardziej poufnego alerty. w takim przypadku czekamy na *5 minut*.
- **Wyślij wiadomość e-mail właściciele i Współautorzy:** w takim przypadku: *włączone*.

Teraz, gdy alert jest tworzony za każdym razem, gdy aplikacja przechodzi przez skonfigurowany próg zostanie wysłana wiadomość e-mail. Aktywne alerty można wyświetlić w taki sposób, w portalu Azure.

![Wyzwalanie alertów](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Dowiedz się więcej o alertach Azure z następujących łączy:
> - [Co to są alerty na platformie Microsoft Azure](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Podejmij działanie metryk](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Tworzenie metryk alertów](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a>Krok 3 — Pomocnik usługi aplikacji
**Pomocnik usługi aplikacji** oferuje wygodny sposób monitorowania aplikacji z natywnym środowiskiem urządzenia przenośnego (z systemem iOS lub Android).

Użyj Pomocnik usługi aplikacji:
- Przejrzyj metryki aplikacji
- Przejrzyj i korzystania z aplikacji, alertów i zalecenia
- Rozwiązywania problemów z podstawowego (Przeglądaj, uruchamianie, zatrzymywanie, ponownie uruchom aplikację)
- Uzyskiwanie powiadomień wypychanych dla zdarzeń krytycznych.

![Pomocnik usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Aplikacja usługi pomocnika sklepu](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Google Play pomocniczy usługi aplikacji](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Pomocnik usługi aplikacji z można zainstalować [sklepu z aplikacjami](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) lub [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a>Krok 4 — diagnozowanie i rozwiązywanie problemów
**Diagnozowanie i rozwiązywanie problemów** pomaga oddzielić problemy aplikacji tworzą problemy platformy. On również zasugerować możliwe ograniczenie jego skutków można pobrać aplikacji sieci Web do dobrej kondycji.

![Diagnozowanie i rozwiązywanie problemów](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Kontynuowaniem przykład formularz poprzednie kroki, zobaczysz, że aplikacja ma zostać problemy dostępności. Natomiast dostępność platformy nie zostały przeniesione od 100%.

Gdy aplikacja ma problem i pozostaje platformy w górę, jest jasne wskazanie, że firma Microsoft ma do czynienia z problemu z aplikacją.

## <a name="logging"></a>Krok 5 — rejestrowanie
Teraz, gdy będziemy mieć zawęzić błędów, aby problemu z aplikacją, możemy obejrzeć Dzienniki aplikacji i serwera, aby uzyskać więcej informacji.

Rejestrowanie umożliwia zbieranie zarówno **programu Application Diagnostics** i **diagnostyki serwera sieci Web** dzienników aplikacji sieci Web.

### <a name="application-diagnostics"></a>Usługa Application Diagnostics
Diagnostyki aplikacji umożliwia przechwytywanie śladów utworzonego przez aplikację w czasie wykonywania.

Dodawanie, śledzenie, aby aplikacja znacznie zwiększa możliwość debugowania i numer pin punktu problemy.

W programie ASP.NET, możesz zalogować się przy użyciu śladów aplikacji [System.Diagnostics.Trace — klasa](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) generowanie zdarzeń, które są przechwytywane przez infrastrukturę dziennika. Można również określić ważność śledzenia łatwiejsze filtrowania.

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
Aby włączyć rejestrowanie aplikacji przejdź do **monitorowanie** > **dzienników diagnostycznych** i włączyć rejestrowania aplikacji za pomocą przełączników.

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Dzienniki aplikacji mogą być przechowywane do aplikacji sieci Web systemu plików lub wypchnięty do magazynu obiektów blob. W scenariuszach produkcyjnym zaleca się używać magazynu obiektów blob.

> [!IMPORTANT]
> Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji. W scenariuszach produkcji zaleca się w dzienniku błędów. Pełniejsze rejestrowanie należy włączyć tylko podczas badania problemów.

 ### <a name="web-server-diagnostics"></a>Diagnostyka serwera sieci Web
Dzienniki serwera sieci Web są generowane, nawet jeśli aplikacja nie została zinstrumentowana. Usługi aplikacji może zbierać trzy różne typy dzienników serwera:

- **Rejestrowanie pracy serwera sieci Web**
    - Informacje o transakcjach HTTP przy użyciu [rozszerzonym formacie W3C dziennika pliku](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Przydatne podczas określania ogólnego metryki lokacji, takie jak liczba żądań obsłużonych lub liczbę żądań pochodzą z określonego adresu IP.
- **Szczegółowe informacje o błędzie logowania**
    - Szczegółowe informacje o błędzie kodów stanu HTTP, które wskazania błędu (kod stanu 400 lub nowszej).
    - [Dowiedz się więcej na temat rejestrowania szczegółowe informacje o błędzie](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Śledzenie niepomyślnych żądań**
    - Szczegółowe informacje dotyczące żądań zakończonych niepowodzeniem, w tym śladu używane do przetwarzania żądania oraz godzinę w poszczególnych składników składników usług IIS.
    - Nie powiodło się żądanie, które dzienniki są przydatne podczas próby izolowania, co powoduje określonego błędu HTTP.
    - [Dowiedz się więcej na temat śledzenia nieudanych żądań](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

Aby włączyć rejestrowanie pracy serwera:
- Przejdź do **monitorowanie** > **dzienników diagnostycznych**.
- Włącz różnego rodzaju diagnostyki serwera sieci Web za pomocą przełączników.

![Monitoruj aplikację](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> Włączanie rejestrowania ma wpływ na wykorzystanie wydajności i zasobów aplikacji. W przypadku scenariuszy produkcji dzienniki błędów są zalecane, włączyć tylko pełniejsze rejestrowanie podczas badania problemów.

### <a name="accessing-logs"></a>Uzyskiwanie dostępu do dzienników
Dzienników przechowywanych w magazynie obiektów blob są dostępne za pomocą Eksploratora usługi Storage platformy Azure. Dzienników przechowywanych w aplikacji sieci Web systemu plików są dostępne za pośrednictwem FTP w następujących ścieżkach:

- **Dzienniki aplikacji** - `%HOME%/LogFiles/Application/`.
    - Ten folder zawiera jeden lub więcej plików tekstowych, zawierający informacje o wygenerowane przez rejestrowanie aplikacji.
- **Nie powiodło się żądanie śladów** - `%HOME%/LogFiles/W3SVC#########/`.
    - Ten folder zawiera plik XSL i co najmniej jeden plik XML.
- **Szczegółowe dzienniki błędów** - `%HOME%/LogFiles/DetailedErrors/`.
    - Ten folder zawiera co najmniej jeden plik .htm o wiele informacji dotyczących błędów HTTP wygenerowany przez aplikację.
- **Dzienniki serwera w sieci Web** - `%HOME%/LogFiles/http/RawLogs`.
    - Ten folder zawiera jeden lub więcej plików tekst sformatowany przy użyciu rozszerzonym formacie W3C dziennika pliku.

## <a name="streaming"></a>Krok 6 - dzienników przesyłania strumieniowego
Dzienniki przesyłania strumieniowego są wygodne podczas debugowania aplikacji, ponieważ zaoszczędzić czas, w porównaniu do [podczas uzyskiwania dostępu do dzienników](#Accessing-Logs) za pośrednictwem FTP.

Usługi aplikacji może być przesyłany strumieniowo **Dzienniki aplikacji** i **dzienniki serwera sieci Web** zgodnie z ich wygenerowaniu.

> [!TIP]
> Przed podjęciem próby strumienia dzienniki, upewnij się, że włączono zbieranie dzienników zgodnie z opisem w [rejestrowanie](#logging) sekcji.

Dzienniki strumieniowo, przejdź do **monitorowanie**> **strumienia dziennika**. Wybierz **Dzienniki aplikacji** lub **dzienniki serwera w sieci Web** zależności informacjach szukasz. W tym miejscu mogą również wstrzymać, uruchom ponownie i wyczyść bufor.

![Dzienniki przesyłania strumieniowego](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Dzienniki są generowane tylko, gdy ruchu w aplikacji, można również zwiększyć poziom szczegółowości dzienniki, aby uzyskać więcej zdarzeń lub informacji.

## <a name="remote"></a>Krok 7. debugowanie zdalne
Kiedy użytkownik ma numer pin — wskazywanej źródło problemów aplikacji, za pomocą **zdalnego debugowania** przechodzenia przez kod.

Zdalne debugowanie umożliwia możesz dołączyć do aplikacji sieci Web uruchomioną w chmurze. Można ustawić punktów przerwania, manipulowanie nimi pamięci bezpośrednio, krokowo kodu oraz nawet zmienić ścieżkę kodu, podobnie jak w przypadku aplikacji uruchomionej na komputerze lokalnym.

Aby dołączyć debuger do aplikacji uruchomionej w chmurze:

- Za pomocą programu Visual Studio 2017 Otwórz rozwiązanie dla aplikacji, którą chcesz debugować
- Ustaw niektórych punktach hamulca, tak jak dla rozwoju lokalnych.
- Otwórz **Eksplorator chmury** (kont. + /, ctrl + x).
- Zaloguj się przy użyciu poświadczeń platformy azure, zgodnie z potrzebami.
- Znajdź aplikację, której chcesz debugować
- Wybierz **dołączyć debuger** formularza **akcje** okienka.

![Debugowanie zdalne](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio konfiguruje aplikację do zdalnego debugowania i uruchamia okno przeglądarki, który nawiguje do aplikacji. Przeglądaj wyzwolenia punktów przerwania i kroku przez kod aplikacji.

> [!WARNING]
> Nie zaleca się uruchamiania w trybie debugowania w środowisku produkcyjnym. Dla wielu wystąpień serwera nie jest skalowanie aplikacji produkcyjnych, debugowanie uniemożliwi serwera sieci web odpowiada na żądania innych. Podczas rozwiązywania problemów w środowisku produkcyjnym, jest najlepszym zasobu [skonfigurować rejestrowanie](#logging) i [usługi Application Insights](#insights).



## <a name="explorer"></a>Krok 8 - Eksploratora procesów
Gdy aplikacja jest skalowana w poziomie do więcej niż jedno wystąpienie **Eksploratora procesów** mogą ułatwić identyfikację wystąpienia określonych problemów.

Użyj **przetworzyć Explorer** do:

- Wylicza wszystkie procesy w różnych wystąpieniach planu usługi aplikacji.
- Przechodzenie i wyświetlić dojścia i moduły skojarzone z każdym procesie.
- Wyświetlanie procesora CPU, zestaw roboczy i liczba na poziomie procesu pomoże zidentyfikować wyczerpania procesów wątków
- Znajdź dojść otwartych plików, a nawet kill wystąpienia określonego procesu.

Eksploratora procesów można znaleźć w **monitorowanie** > **Eksploratora procesów**.

![Eksplorator procesów](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a>Krok 9 - usługi Application Insights
**Usługa Application Insights** zapewnia profilowania aplikacji i zaawansowanych możliwości monitorowania dla aplikacji.

Usługa Application Insights umożliwia wykrywanie i diagnozowanie wyjątków i problemy z wydajnością w aplikacji sieci Web.

Można włączyć usługi Application Insights dla aplikacji sieci Web, w obszarze **monitorowanie** > **usługi Application Insights**

> [!NOTE]
> Usługa Application Insights może monit o zainstalowanie rozszerzenia lokacji usługi Application Insights, aby rozpocząć zbieranie danych. Instalowanie rozszerzenia lokacji powoduje ponowne uruchomienie aplikacji.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Usługa Application Insights ma zaawansowanych funkcji, ustawić, aby dowiedzieć się więcej, skorzystaj z łączy zawarte w [następne kroki](#next) sekcji.

## <a name="next"></a> Następne kroki

 - [Co to jest usługa Application Insights](..\application-insights\app-insights-overview.md)
 - [Monitorowanie wydajności aplikacji sieci web platformy Azure przy użyciu usługi Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Monitorowanie dostępności i szybkość reakcji każdej witrynie sieci web z usługą Application Insights](..\application-insights\app-insights-monitor-web-app-availability.md)
