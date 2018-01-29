---
title: "Najlepsze rozwiązania i w podręczniku rozwiązywania problemów z węzła aplikacje aplikacji sieci Web Azure"
description: "Dowiedz się, najlepszych rozwiązań i kroki rozwiązywania problemów z węzła aplikacje na platformie Azure aplikacje sieci Web."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/09/2017
ms.author: ranjithr
ms.openlocfilehash: f7f3186ba93670e566a10f97dde86a977101e8fc
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Najlepsze rozwiązania i w podręczniku rozwiązywania problemów z węzła aplikacje aplikacji sieci Web Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

W tym artykule dowiesz się najlepszych rozwiązań i kroki rozwiązywania problemów z [węzła aplikacje](app-service-web-get-started-nodejs.md) uruchomiona na platformie Azure aplikacje sieci Web (o [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Przy użyciu kroków w swojej witrynie produkcji, należy zachować ostrożność. Zalecanie służy do rozwiązywania problemów z aplikacją w Instalator nieprodukcyjnych na przykład Twoje miejsce przemieszczania, a jeśli problem został rozwiązany, zamienić Twoje miejsce wystawiania z Twojego miejsca produkcji.
> 
> 

## <a name="iisnode-configuration"></a>Konfiguracja programu IISNODE
To [pliku schematu](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) zawiera wszystkie ustawienia, można skonfigurować dla programu iisnode. Niektóre ustawienia, które są przydatne w przypadku aplikacji:

* nodeProcessCountPerApplication
  
    To ustawienie określa liczbę procesów węzła, które będą uruchamiane na aplikacji usług IIS. Wartość domyślna to 1. Można uruchomić dowolną liczbę node.exes jako liczba vCPU sieci maszyn wirtualnych przez ustawienie to 0. Zalecana wartość to 0 dla większości aplikacji, dzięki czemu można używać wszystkich Vcpu na tym komputerze. Node.exe jest jednowątkowy tak maksymalnie 1 vCPU zużywa jeden node.exe. Aby uzyskać maksymalną wydajność poza aplikacji węzła, chcesz użyć wszystkich Vcpu.
* nodeProcessCommandLine
  
    To ustawienie określa ścieżkę do node.exe. Można ustawić tej wartości, aby wskazywał wersji node.exe.
* maxConcurrentRequestsPerProcess
  
    To ustawienie określa maksymalną liczbę jednoczesnych żądań wysłanych przez program iisnode do każdego node.exe. Na platformie Azure aplikacje sieci Web wartość domyślna to jest bez ograniczeń czasowych. Nie trzeba martwić się o tym ustawieniu. Poza Azure Web Apps wartość domyślna to 1024. Można to skonfigurować, w zależności od liczby żądań, aplikacja odbiera i tempa aplikacji przetwarzania każdego żądania.
* maxNamedPipeConnectionRetry
  
    To ustawienie określa maksymalną liczbę razy iisnode ponownych prób nawiązywania połączenia przez nazwany potok do wysłania żądania do node.exe. To ustawienie w połączeniu z namedPipeConnectionRetryDelay określa całkowity limit czasu każdego żądania w ramach programu iisnode. Wartość domyślna to 200 aplikacji sieci Web platformy Azure. Całkowity limit czasu w sekundach = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    To ustawienie określa ilość czasu (w ms) czeka iisnode między kolejnymi próbami można wysłać żądania do node.exe za pomocą potoku nazwanego. Wartość domyślna to 250 ms.
    Całkowity limit czasu w sekundach = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    Domyślnie łącznego limitu czasu w iisnode aplikacji sieci Web platformy Azure jest 200 \* 250 ms = 50 sekund.
* logDirectory
  
    To ustawienie określa katalog, w którym program iisnode rejestruje stdout/stderr. Wartość domyślna to iisnode, która jest względem katalogu głównego skryptu (gdzie występuje server.js głównego katalogu)
* debuggerExtensionDll
  
    To ustawienie określa, która wersja narzędzia node-inspector iisnode używa podczas debugowania aplikacji węzła. Obecnie program iisnode inspektora 0.7.3.dll i iisnode inspector.dll są jedyne prawidłowe wartości dla tego ustawienia. Wartość domyślna to iisnode inspektora 0.7.3.dll. Wersja programu iisnode inspektora 0.7.3.dll używa 0.7.3-node-inspector i używa protokołu websocket. Należy włączyć protokół websockets na Azure aplikacji sieci Web do użycia tej wersji. Zobacz <http://www.ranjithr.com/?p=98> Aby uzyskać więcej informacji na temat konfigurowania programu iisnode, aby użyć nowego narzędzia node-inspector.
* flushResponse
  
    Domyślne zachowanie usług IIS jest buforuje dane odpowiedzi na górę 4 MB przed opróżnianie lub aż do zakończenia odpowiedzi, zależnie od zostanie osiągnięty jako pierwszy. iisnode oferuje ustawienie konfiguracji, aby zmienić to zachowanie: Aby opróżnić fragment treści jednostki odpowiedzi, jak program iisnode odbiera on z node.exe, należy ustawić iisnode/@flushResponse atrybutu w pliku web.config na wartość "true":
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Włączanie opróżnianie każdego fragmentu odpowiedzi treści jednostki zwiększa wydajność ograniczającą przepływności systemu % ~ 5 (począwszy od v0.1.13), dlatego najlepiej zakres to ustawienie tylko dla punktów końcowych, które wymagają odpowiedzi przesyłania strumieniowego (na przykład za pomocą <location> elementu w pliku web.config).
  
    Oprócz tego do przesyłania strumieniowego aplikacji, należy także ustawić responseBufferLimit Twojego programu iisnode obsługi na 0.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Jest to rozdzielana średnikami lista plików, które są monitorowane zmian. Zmiany w pliku powoduje, że aplikacja do odtworzenia. Każdy wpis zawiera nazwę katalogu opcjonalne oraz nazwę pliku wymagane są względem katalogu, w którym znajduje się punkt wejścia aplikacji głównej. Symbole wieloznaczne są dozwolone w tylko części nazwy pliku. Wartość domyślna to "\*. js;web.config"
* recycleSignalEnabled
  
    Wartość domyślna to false. Włączenie aplikacji węzła można nawiązać połączenia nazwanego potoku (zmienną środowiskową IISNODE\_kontroli\_POTOKU) i wysłać wiadomość "odtworzenia". Powoduje to w3wp do odtworzenia bezpiecznie zamknąć.
* idlePageOutTimePeriod
  
    Wartość domyślna to 0, co oznacza, że ta funkcja jest wyłączona. Gdy ustawiona niektórych wartość większą niż 0, iisnode będzie strony się jego procesy podrzędne co "idlePageOutTimePeriod" (w milisekundach). Zobacz [dokumentacji](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx) zrozumieć, co strony limit środków. To ustawienie jest przydatne w przypadku aplikacji, które zużywają dużej ilości pamięci i strona limit pamięci na dysku, co pewien czas, aby zwolnić niektóre pamięci RAM.

> [!WARNING]
> Należy zachować ostrożność podczas włączania następujące ustawienia konfiguracji w przypadku aplikacji produkcyjnej. Zaleca się nie je włączyć w przypadku aplikacji produkcyjnej na żywo.
> 
> 

* debugHeaderEnabled
  
    Wartość domyślna to false. Jeśli ustawiono wartość true, iisnode dodaje HTTP odpowiedzi nagłówka iisnode debugowania do każdej odpowiedzi HTTP wysyła się, że wartość nagłówka debugowania programu iisnode jest adresem URL. Pojedynczych informacji diagnostycznych może zgromadzone analizując fragmentu adresu URL, ale jest to osiągane przez otwierania adresu URL w przeglądarce dużo lepsze wizualizacje.
* loggingEnabled
  
    To ustawienie określa rejestrowanie stdout i stderr przez program iisnode. Iisnode przechwytuje stdout/stderr z węzła procesów go uruchamia i zapisuje w katalogu określonym w ustawieniu "logDirectory". Gdy ta opcja jest włączona, aplikacja zapisuje dzienniki w systemie plików i w zależności od ilości rejestrowania wykonywane przez aplikację, może mieć wpływ na wydajność.
* devErrorsEnabled
  
   Wartość domyślna to false. Gdy ustawiona na wartość true, iisnode Wyświetla kod stanu HTTP i kod błędu Win32 w przeglądarce. Kod win32 jest przydatne w debugowaniu niektóre rodzaje problemów.
* debuggingEnabled (nie należy włączać w witrynie produkcyjnym)
  
    To ustawienie określa funkcja debugowania. Program Iisnode jest zintegrowany z narzędzia node-inspector. Po włączeniu tego ustawienia, należy włączyć debugowanie aplikacji węzła. Po włączeniu tego ustawienia program iisnode będzie układ niezbędne narzędzia node-inspector plików w katalogu "debuggerVirtualDir" na pierwsze żądanie debugowania do węzła aplikacji. Można załadować narzędzia node-inspector, wysyłając żądanie do http://yoursite/server.js/debug. Segment adresu URL debugowania można kontrolować z ustawieniem "debuggerPathSegment". Domyślnie debuggerPathSegment = "debugowanie". Możesz ustawić na identyfikator GUID, na przykład, aby trudniej mają zostać wykryte przez innych użytkowników.
  
    Sprawdź [łącze](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) uzyskać więcej informacji dotyczących debugowania.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Scenariusze i zalecenia/Rozwiązywanie problemów
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Moja aplikacja węzła jest wprowadzenie zbyt wiele wywołań wychodzących.
Wiele aplikacji warto, aby nawiązywać połączenia wychodzące w ramach ich regularnych operacji. Na przykład gdy nadejdzie żądanie, węzeł aplikacji warto, aby skontaktować się z interfejsu API REST w innym miejscu i niektóre informacje do przetwarzania żądania. Czy chcesz użyć agenta keep alive wywołania protokołu http lub https. Na przykład można użyć modułu programu agentkeepalive jako keep alive agenta, podczas wprowadzania tych wywołań wychodzących. Dzięki temu, że w sieci Azure aplikacji sieci Web maszyny Wirtualnej nie są ponownie gniazdami i zmniejsza obciążenie związane z tworzenia nowych gniazd dla każdego żądania wychodzącego. Ponadto dzięki temu się, że używasz mniejszą liczbę gniazd, aby wprowadzić wiele żądań wychodzących i dlatego nie może przekraczać ustawienie maxSockets, które są przydzielone dla maszyny Wirtualnej. W aplikacji sieci Web Azure zaleca się wartość agentKeepAlive ustawienie maxSockets łącznie 160 gniazda dla maszyny Wirtualnej. Oznacza to, jeśli masz cztery node.exe uruchomione na maszynie Wirtualnej, chcesz ustawić ustawienie maxSockets agentKeepAlive 40 za node.exe, który jest 160 całkowita dla maszyny Wirtualnej.

Przykład [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) konfiguracji:

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

W tym przykładzie przyjęto założenie, że masz 4 node.exe uruchomione na maszynie Wirtualnej. Jeśli masz inną liczbę node.exe uruchomione na maszynie Wirtualnej, należy zmodyfikować ustawienie maxSockets, w związku z tym ustawieniem.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Moja aplikacja węzła zużywa zbyt dużej ilości Procesora.
Prawdopodobnie zostanie wyświetlone zalecenie z aplikacji sieci Web platformy Azure w portalu sieci o wysokie użycie procesora cpu. Można także skonfigurować monitory do monitorowania określonych [metryki](web-sites-monitor.md). Podczas sprawdzania użycia procesora CPU na [pulpitu nawigacyjnego portalu Azure](../application-insights/app-insights-web-monitor-performance.md), sprawdź wartości MAX dla Procesora, dzięki czemu nie traci wartości szczytowe.
W przypadkach, gdy uważasz, że aplikacja zużywa zbyt dużej ilości procesora CPU i nie można wyjaśnić, dlaczego może profilu aplikacji węzeł, aby dowiedzieć się.

### 
#### <a name="profiling-your-node-application-on-azure-web-apps-with-v8-profiler"></a>Profilowanie aplikacji węzła aplikacji sieci Web platformy Azure z V8 profilera
Załóżmy na przykład, że aplikacja world hello przewidzianą do profilowania w następujący sposób:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Przejdź do Twojej scm https://yoursite.scm.azurewebsites.net/DebugConsole lokacji

Wiersz polecenia możesz sprawdzić, jak pokazano poniżej. Przejdź do katalogu witryny/wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Uruchom polecenie "npm install v8 profilera".

To należy instalować programu profilującego v8 w węźle\_modułów katalogu i wszystkich jego zależności.
Teraz Edytuj server.js sieci do profilu aplikacji.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Poprzedni kod profile WriteConsoleLog funkcji, a następnie zapisuje dane wyjściowe profilu do pliku "profile.cpuprofile" w obszarze wwwroot z lokacji. Wyślij żądanie do aplikacji. Możesz zobaczyć plik "profile.cpuprofile" utworzone na podstawie wwwroot Twojej lokacji.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Pobierz ten plik i otwórz go z narzędziami F12 Chrome. Naciśnij klawisz F12 w Chrome, a następnie wybierz pozycję **profile** kartę. Wybierz **obciążenia** przycisku. Wybierz plik profile.cpuprofile pobrany. Kliknij żądany profil załadowane przed chwilą.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Widać, że 95% czasu został wykorzystany przez funkcję WriteConsoleLog. To również wyświetlanie numerów wierszy dokładne i plików źródłowych, która spowodowała problem.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Moja aplikacja węzła zużywa zbyt dużej ilości pamięci
Jeśli aplikacja zużywa zbyt dużej ilości pamięci, zobaczysz powiadomienie z aplikacji sieci Web platformy Azure w portalu sieci o duże użycie pamięci. Możesz skonfigurować monitory do monitorowania określonych [metryki](web-sites-monitor.md). Podczas sprawdzania użycia pamięci na [pulpitu nawigacyjnego portalu Azure](../application-insights/app-insights-web-monitor-performance.md), sprawdź wartości maksymalna wartość pamięci, dzięki czemu nie traci wartości szczytowe.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Wykrywanie przecieków i porównywania sterty dla środowiska node.js
Można użyć [memwatch węzła](https://github.com/lloyd/node-memwatch) pomoże zidentyfikować pamięci przecieków.
Można zainstalować memwatch podobnie jak profilera v8 i edytować kod do przechwytywania i różnicowy stosów do identyfikowania pamięć przecieków w aplikacji.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Moje node.exe są pobierania losowo skasowane.
Istnieje kilka przyczyn, dlaczego może to występować:

1. Aplikacji wywołującej nieprzechwyconych wyjątków — d: wyboru\\macierzystego\\LogFiles\\aplikacji\\errors.txt rejestrowania w pliku na wyjątek. Ten plik zawiera ślad stosu, więc można naprawić na podstawie tych aplikacji.
2. Aplikacja zużywa zbyt dużej ilości pamięci, co ma wpływ na inne procesy z wprowadzenie. Jeśli łączna ilość pamięci maszyny Wirtualnej jest bliski 100%, Twoje node.exe można kasować przez Menedżera procesu, aby umożliwić inne procesy, które umożliwiają wykonania dodatkowych czynności. Aby rozwiązać ten problem, upewnij się, że aplikacja nie jest przeciek pamięci albo jeśli aplikacja wymaga dużą ilość pamięci, skalowanie w górę do większych maszyn wirtualnych ze znacznie większą ilość pamięci RAM.

### <a name="my-node-application-does-not-start"></a>Moja aplikacja węzła nie uruchamia.
Jeśli aplikacja zwraca błędy 500 podczas uruchamiania, może istnieć kilka przyczyn:

1. Node.exe nie jest obecny w poprawnej lokalizacji. Sprawdź ustawienie nodeProcessCommandLine.
2. Plik skryptu głównego nie ma w poprawnej lokalizacji. Sprawdź plik web.config i upewnij się, że nazwa pliku głównego skryptu w sekcji obsługi pasuje do pliku głównego skryptu.
3. Plik Web.config konfiguracji jest niepoprawna — sprawdzanie nazw/wartości ustawień.
4. Zimny Start — aplikacji trwa zbyt długo, aby rozpocząć. Jeśli aplikacja będzie trwało dłużej niż (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1 000 sekund iisnode zwraca błąd 500. Zwiększenie wartości tych ustawień, aby dopasować godziną początkową aplikacji, aby zapobiec iisnode limit czasu i zwróceniem komunikatu o błędzie 500.

### <a name="my-node-application-crashed"></a>Moja aplikacja węzła awaria
Aplikacji wywołującej nieprzechwyconych wyjątków — d: wyboru Sprawdź\\macierzystego\\LogFiles\\aplikacji\\errors.txt rejestrowania w pliku na wyjątek. Ten plik zawiera ślad stosu, więc można naprawić na podstawie tych aplikacji.

### <a name="my-node-application-takes-too-much-time-to-start-cold-start"></a>Moja aplikacja węzeł ma zbyt dużo czasu, aby uruchomić (zimny Start)
Najczęstszą przyczyną zbyt długiego czasu uruchomienia aplikacji jest wysoka liczba plików w węźle\_modułów. Aplikacja próbuje załadować większość tych plików, podczas uruchamiania. Domyślnie ponieważ pliki znajdują się w udziale sieciowym, aplikacji sieci Web platformy Azure, podczas ładowania wielu plików może trwać.
Dostępne są następujące rozwiązania przyspieszyć ten proces:

1. Upewnij się, że masz struktury płaskiej zależności i ma zduplikowane zależności za pomocą npm3 własnych modułów.
2. Próba opóźnionego ładowania węzeł\_moduły i nie ładować wszystkie moduły podczas uruchamiania aplikacji. Oznacza to, że wywołanie require('module') należy dokonać Jeśli faktycznie wymagane w ramach funkcji, do której zostanie podjęta, gdy za pomocą modułu.
3. Aplikacje sieci Web platformy Azure oferuje funkcję o nazwie lokalnej pamięci podręcznej. Ta funkcja kopiuje zawartość z udziału sieciowego na lokalny dysk na maszynie Wirtualnej. Ponieważ pliki znajdują się lokalnie, czas ładowania węzła\_modułów jest znacznie szybsze.

## <a name="iisnode-http-status-and-substatus"></a>Stan http IISNODE i podstanu
To [plik źródłowy](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) Wyświetla wszystkie możliwe stan/podstanu iisnode kombinacji może zwrócić w przypadku błędu.

Włącz FREB dla aplikacji, aby zobaczyć kod błędu win32 (należy włączyć FREB tylko w lokacjach nieprodukcyjnych ze względu na wydajność).

| Stan HTTP | Podstan protokołu HTTP | Możliwa przyczyna? |
| --- | --- | --- |
| 500 |1000 |Znaleziono niektórych problem podczas wysyłania żądania do programu IISNODE — Sprawdź, czy node.exe został uruchomiony. Node.exe może ulec awarii podczas uruchamiania. Sprawdź konfigurację web.config błędów. |
| 500 |1001 |-Win32Error 0x2 — aplikacja nie odpowiada na adres URL. Sprawdź reguły ponownego zapisywania adresów URL lub wyboru, jeśli aplikacja express ma poprawne trasy zdefiniowane. -Win32Error 0x6d — nazwany potok jest zajęty — Node.exe nie akceptuje żądania potoku jest zajęty. Sprawdź wysokiego użycia procesora cpu. -Inne błędy — Sprawdź, czy awaria node.exe. |
| 500 |1002 |Awaria node.exe — sprawdź d:\\macierzystego\\LogFiles\\rejestrowania errors.txt dla ślad stosu. |
| 500 |1003 |Potok konfiguracji problem — nigdy nie powinno to zobaczyć, ale jeśli to zrobisz, konfiguracja nazwany potok jest niepoprawna. |
| 500 |1004-1018 |Wystąpił błąd podczas wysyłania żądania lub odpowiedzi z node.exe przetwarzania. Sprawdź, czy awaria node.exe. Sprawdź d:\\macierzystego\\LogFiles\\rejestrowania errors.txt dla ślad stosu. |
| 503 |1000 |Za mało pamięci, aby przydzielić więcej połączeń nazwanych potoków. Sprawdź, dlaczego aplikacja zużywa dużej ilości pamięci. Sprawdź wartość ustawienia maxConcurrentRequestsPerProcess. Jeśli masz wiele żądań nie jest nieograniczony, należy zwiększyć tę wartość, aby uniknąć tego błędu. |
| 503 |1001 |Nie można wysłać żądania do node.exe, ponieważ aplikacja jest odtwarzania. Po aplikacji po odtworzeniu, żądania powinien być obsługiwany normalnie. |
| 503 |1002 |Kod błędu win32 wyboru przyczyny rzeczywiste — żądanie nie mógł zostać wysłany do node.exe. |
| 503 |1003 |Nazwany potok jest zbyt zajęty — Sprawdź, jeśli węzeł zużywa zbyt Procesora |

Ustawienie w NODE.exe węzeł\_OCZEKUJE\_POTOKU\_WYSTĄPIEŃ. Domyślnie poza Azure Web Apps ta wartość to 4. Oznacza to, że ten node.exe jednocześnie na nazwanym potoku może akceptować tylko żądania cztery. Na platformie Azure aplikacje sieci Web ta wartość jest równa 5000. Ta wartość powinna być wystarczająca dla większości aplikacji węzła uruchomiona na platformie Azure aplikacje sieci Web. Użytkownik nie powinien być widoczny 503.1003 aplikacji sieci Web Azure ze względu na wysoką wartość dla węzła\_OCZEKUJE\_POTOKU\_WYSTĄPIEŃ.  |

## <a name="more-resources"></a>Więcej zasobów
Skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat aplikacji node.js w usłudze Azure App Service.

* [Rozpoczynanie pracy z aplikacjami sieci Web Node.js w usłudze Azure App Service](app-service-web-get-started-nodejs.md)
* [How to debug a Node.js web app in Azure App Service (Jak debugować aplikację sieci Web Node.js w usłudze Azure App Service)](app-service-web-tutorial-nodejs-mongodb-app.md)
* [Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps: Node.js (Aplikacje sieci Web w usłudze Azure App Service: Node.js)](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centrum deweloperów środowiska Node.js](../nodejs-use-node-modules-azure-apps.md)
* [Exploring the Super Secret Kudu Debug Console (Szczegółowe informacje o ściśle tajnej konsoli debugowania aparatu Kudu)](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

