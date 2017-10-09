---
title: "aaaBest rozwiązań i w podręczniku rozwiązywania problemów z węzła aplikacje aplikacji sieci Web Azure"
description: "Dowiedz się hello najlepszych rozwiązań i kroki rozwiązywania problemów z węzła aplikacje na platformie Azure aplikacje sieci Web."
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
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Najlepsze rozwiązania i w podręczniku rozwiązywania problemów z węzła aplikacje aplikacji sieci Web Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

W tym artykule dowiesz się hello najlepszych rozwiązań i kroki rozwiązywania problemów z [węzła aplikacje](app-service-web-get-started-nodejs.md) systemem Azure Webapps (z [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Przy użyciu kroków w swojej witrynie produkcji, należy zachować ostrożność. Zalecane jest tootroubleshoot aplikacji na nieprodukcyjnych na przykład skonfigurować Twoje miejsce wystawiania i gdy problemu hello wymiany Twoje miejsce wystawiania z Twojego miejsca produkcji.
> 
> 

## <a name="iisnode-configuration"></a>Konfiguracja programu IISNODE
To [pliku schematu](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) zawiera wszystkie ustawienia hello, które można skonfigurować dla programu iisnode. Niektóre ustawienia hello, które będą przydatne w przypadku aplikacji są:

* nodeProcessCountPerApplication
  
    To ustawienie określa hello liczbę procesów węzła, które będą uruchamiane na aplikacji usług IIS. Wartość domyślna to 1. Przez ustawienie to too0 można uruchomić dowolną liczbę node.exe jako liczba rdzeni sieci maszyn wirtualnych. Zalecana wartość to 0 dla większości aplikacji, więc można korzystać ze wszystkich rdzeni hello na tym komputerze. Node.exe jest pojedynczym wątku, co node.exe będą korzystać z maksymalnie 1 rdzeni i tooget maksymalną wydajność poza węzeł aplikacji warto tooutilize wszystkich rdzeni.
* nodeProcessCommandLine
  
    To ustawienie określa hello ścieżki toohello node.exe. Można ustawić tej wartości toopoint tooyour node.exe wersji.
* maxConcurrentRequestsPerProcess
  
    To ustawienie określa maksymalną liczbę równoczesnych żądań wysłanych przez program iisnode tooeach node.exe hello. Na używanie azure hello wartość domyślna to jest bez ograniczeń czasowych. Nie trzeba tooworry o tym ustawieniu. Poza azure webapps hello wartość domyślna to 1024. Możesz tooconfigure, który pobiera to w zależności od tego, ile żądań aplikacji i tempa aplikacji przetwarzania każdego żądania.
* maxNamedPipeConnectionRetry
  
    To ustawienie określa maksymalną liczbę razy iisnode ponowi próbę połączenia wprowadzania na powitania o nazwie potoku toosend hello żądanie za pośrednictwem toonode.exe hello. To ustawienie w połączeniu z namedPipeConnectionRetryDelay określa hello łącznego limitu czasu każdego żądania w ramach programu iisnode. Wartość domyślna to 200 na używanie usługi Azure. Całkowity limit czasu w sekundach = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    Ustawienie formanty hello ilość czasu (w ms) iisnode będzie oczekiwał na między każdego toonode.exe żądania toosend ponów próbę za pośrednictwem hello nazwany potok. Wartość domyślna to 250ms.
    Całkowity limit czasu w sekundach = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    Domyślnie hello łącznego limitu czasu w iisnode na używanie azure to 200 \* 250ms = 50 sekund.
* logDirectory
  
    To ustawienie określa, gdzie iisnode będzie rejestrować stdout/stderr katalogu hello. Wartość domyślna to iisnode, który jest katalogiem głównym skryptu względną toohello (gdzie występuje server.js głównego katalogu)
* debuggerExtensionDll
  
    To ustawienie określa, jakie wersji narzędzia node-inspector iisnode będzie używany podczas debugowania aplikacji węzła. Obecnie iisnode inspektora 0.7.3.dll i iisnode inspector.dll są hello 2 tylko prawidłowe wartości dla tego ustawienia. Wartość domyślna to iisnode inspektora 0.7.3.dll. wersja programu iisnode inspektora 0.7.3.dll używa 0.7.3-node-inspector i używa protokołu websocket, więc należy tooenable websocket w Twojej aplikacji sieci Web azure toouse tej wersji. Zobacz <http://www.ranjithr.com/?p=98> uzyskać więcej informacji dotyczących sposobu tooconfigure iisnode toouse hello nowe narzędzia node-inspector.
* flushResponse
  
    Witaj domyślne zachowanie usług IIS nie buforuje dane odpowiedzi na górę too4MB przed opróżnianie, lub do końca hello hello odpowiedzi, zależnie od zostanie osiągnięty jako pierwszy. iisnode oferuje ustawienie toooverride to zachowanie konfiguracji: tooflush fragment treści jednostki hello odpowiedź tak szybko, jak program iisnode odbiera on z node.exe należy tooset hello iisnode/@flushResponse atrybutu w pliku web.config too'true ":
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Włączanie opróżnianie każdego fragmentu treść jednostki odpowiedzi hello zwiększa wydajność ograniczającą przepływności hello hello systemu % ~ 5 (począwszy od v0.1.13), dlatego najlepszym tooscope tego tooendpoints tylko ustawienie, które wymagają odpowiedzi przesyłania strumieniowego (np. przy użyciu hello <location> elementu w pliku web.config hello)
  
    W toothis dodanie do przesyłania strumieniowego aplikacji, konieczne będzie tooalso responseBufferLimit zestawu z programu iisnode too0 programu obsługi.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Jest to rozdzielana średnikami lista plików, które będą monitorowane zmian. Zmienianie pliku tooa powoduje, że toorecycle aplikacji hello. Każdy wpis składa się z nazwy katalogu opcjonalne i nazwy wymaganego pliku, która są katalog toohello względny, w którym znajduje się punkt wejścia aplikacji głównej hello. Symbole wieloznaczne są dozwolone w tylko część nazwy pliku hello. Wartość domyślna to "\*. js;web.config"
* recycleSignalEnabled
  
    Wartość domyślna to false. U możliwia aplikacji węzła można połączyć tooa nazwany potok (zmienną środowiskową IISNODE\_kontroli\_POTOKU) i wysłać wiadomość "odtworzenia". Spowoduje to hello w3wp toorecycle bezpiecznie zamknąć.
* idlePageOutTimePeriod
  
    Wartość domyślna to 0, co oznacza, że ta funkcja jest wyłączona. Gdy zestaw toosome wartość większą niż 0, iisnode będzie strony się jego podrzędny przetwarza co milisekund "idlePageOutTimePeriod". toounderstand co strony limit oznacza, zobacz toothis [dokumentacji](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). To ustawienie będzie przydatna dla aplikacji, które zużywają dużej ilości pamięci i mają toodisk pamięci toopageout czasami toofree pamięć RAM niektórych.

> [!WARNING]
> Należy zachować ostrożność podczas włączania hello następujące ustawienia konfiguracji w przypadku aplikacji produkcyjnej. Zalecane jest toonot Włącz aplikacji produkcyjnych na żywo.
> 
> 

* debugHeaderEnabled
  
    Witaj wartość domyślna to false. Jeśli wartość tootrue, iisnode doda odpowiedzi nagłówka debugowania programu iisnode tooevery HTTP odpowiedzi HTTP wysyła wartość nagłówka debugowania programu iisnode hello jest adresem URL. Poszczególne informacje diagnostyczne dotyczące można zgromadzone analizując hello fragmentu adresu URL, ale otwierając hello adresu URL w przeglądarce hello uzyskuje się znacznie lepsze wizualizacje.
* loggingEnabled
  
    To ustawienie określa rejestrowanie hello stdout i stderr przez program iisnode. Iisnode będzie przechwytywać stdout/stderr z procesów węzła, który jest uruchamiany i zapisu katalogu toohello określona w ustawieniu "logDirectory" hello. Po to jest włączona, aplikacja będzie zapisywania toohello dzienniki w systemie plików, a następnie w zależności od ilości hello rejestrowania programach aplikacji hello, może być wpływ na wydajność.
* devErrorsEnabled
  
    Wartość domyślna to false. Po ustawieniu tootrue, iisnode wyświetli kod stanu hello HTTP i kod błędu Win32 w przeglądarce. Kod win32 Hello będzie pomocnych w debugowaniu niektóre rodzaje problemów.
* debuggingEnabled (nie należy włączać w witrynie produkcyjnym)
  
    To ustawienie określa funkcja debugowania. Program Iisnode jest zintegrowany z narzędzia node-inspector. Po włączeniu tego ustawienia, należy włączyć debugowanie aplikacji węzła. Po włączeniu tego ustawienia program iisnode będzie układu hello niezbędne narzędzia node-inspector plików w katalogu "debuggerVirtualDir" na powitania pierwszej debugowania żądania tooyour węzła aplikacji. Można załadować narzędzia node-inspector hello wysyłając toohttp://yoursite/server.js/debug żądania. Segment adresu URL debugowania hello można kontrolować z ustawieniem "debuggerPathSegment". Domyślne debuggerPathSegment = "debugowanie". Ta tooa identyfikator GUID, na przykład można ustawić tak, aby trudniejsze toobe odnalezione przez innych użytkowników.
  
    Sprawdź [łącze](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) uzyskać więcej informacji dotyczących debugowania.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Scenariusze i zalecenia/Rozwiązywanie problemów
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Moja aplikacja węzła jest wprowadzenie zbyt wiele wywołań wychodzących.
Wiele aplikacji warto toomake połączeń wychodzących, w ramach ich regularnych operacji. Na przykład gdy nadejdzie żądanie, aplikację węzła czy mają toocontact interfejsu API REST w innym miejscu i pobrać niektóre informacje tooprocess hello żądania. Czy chcesz toouse agenta keep alive wywołania protokołu http lub https. Można na przykład użyć modułu agentkeepalive hello jako keep alive agenta, podczas wprowadzania tych wywołań wychodzących. Dzięki temu się upewnić, że hello sockets są ponownie w tej aplikacji sieci Web azure maszyny Wirtualnej i zmniejszenie obciążenia hello tworzenia nowych gniazd dla każdego żądania wychodzącego. Dzięki temu też się upewnić, że używasz mniejszą liczbę toomake sockets wiele żądań wychodzących i dlatego nie przekraczają ustawienie maxSockets hello, które są przydzielone dla maszyny Wirtualnej. Zalecenie dotyczące Azure Webapps mogą być ustawienie maxSockets agentKeepAlive hello tooset wartości całkowitej tooa 160 gniazd dla maszyny Wirtualnej. Oznacza to, że jeśli masz 4 node.exe systemem hello wirtualna byłaby wskazana tooset hello agentKeepAlive ustawienie maxSockets too40 na node.exe czyli 160 całkowita dla maszyny Wirtualnej.

Przykład [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) konfiguracji:

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

W tym przykładzie przyjęto założenie, że masz 4 node.exe uruchomione na maszynie Wirtualnej. Jeśli masz inną liczbę node.exe systemem hello maszyny Wirtualnej, konieczne będzie ustawienie maxSockets hello toomodify odpowiednio ustawienia.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Moja aplikacja węzła zużywa zbyt dużej ilości Procesora.
Zalecenia w Azure Webapps prawdopodobnie zostanie wyświetlony w portalu sieci o wysokie użycie procesora cpu. Możesz również toowatch monitory konfiguracji dla niektórych [metryki](web-sites-monitor.md). Podczas sprawdzania użycia procesora CPU hello na powitania [pulpitu nawigacyjnego portalu Azure](../application-insights/app-insights-web-monitor-performance.md), sprawdź, czy wartości maksymalnej hello procesora CPU, nie zostały pominięte wartości szczytowe hello.
W przypadkach, gdy uważasz, że aplikacja zużywa zbyt dużej ilości procesora CPU i nie można wyjaśnić, dlaczego należy tooprofile aplikacji węzła.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Profilowanie aplikacji węzła na używanie azure z V8 profilera
Na przykład umożliwia powiedz aplikacja hello world mają tooprofile, jak pokazano poniżej:

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

Przejdź tooyour scm lokacji https://yoursite.scm.azurewebsites.net/DebugConsole

Zobaczysz wiersz polecenia, jak pokazano poniżej. Przejdź do katalogu witryny/wwwroot

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Uruchom polecenie Witaj, "npm install v8 profilera"

To należy instalować programu profilującego v8 w węźle\_modułów katalogu i wszystkich jego zależności.
Teraz Edytuj tooprofile Twojego server.js aplikacji.

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

Hello powyżej zmiany będą profilu hello WriteConsoleLog funkcji, a następnie wpisz hello profilu dane wyjściowe too'profile.cpuprofile "plik w Twojej lokacji wwwroot. Wyślij żądanie tooyour aplikacji. Zostanie wyświetlony plik 'profile.cpuprofile' utworzone na podstawie wwwroot z lokacji.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Pobierz ten plik i trzeba będzie tooopen ten plik przy użyciu narzędzia F12 Chrome. Trafienia F12 na chrome, a następnie kliknij na powitania "Kartę Profile". Kliknij przycisk "Obciążenia". Wybierz plik profile.cpuprofile, który został pobrany. Kliknij profil hello załadowane przed chwilą.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Zobaczysz, że 95% czasu hello została wykorzystana przez WriteConsoleLog funkcji, jak pokazano poniżej. To również zawiera numery wierszy dokładne hello i plików źródłowych, których przyczyną problemu hello.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Moja aplikacja węzła zużywa zbyt dużej ilości pamięci.
Zalecenia w Azure używanie prawdopodobnie zostanie wyświetlony w portalu sieci o duże użycie pamięci. Możesz również toowatch monitory konfiguracji dla niektórych [metryki](web-sites-monitor.md). Podczas sprawdzania użycia pamięci hello na powitania [pulpitu nawigacyjnego portalu Azure](../application-insights/app-insights-web-monitor-performance.md), dzięki czemu nie traci wartości szczytowe hello Sprawdź hello wartości maksymalnej pamięci.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Wykrywanie przecieków i porównywania sterty dla środowiska node.js
Można użyć [memwatch węzła](https://github.com/lloyd/node-memwatch) przecieków toohelp zidentyfikować pamięci.
Należy zainstalować memwatch podobnie jak profilera v8 i edycji przez użytkownika kod toocapture i różnicowy stosów tooidentify hello wyciek pamięci w aplikacji.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Moje node.exe są pobierania losowo skasowane.
Istnieje kilka przyczyn, dlaczego może to występować:

1. Aplikacji wywołującej nieprzechwyconych wyjątków — d: wyboru Sprawdź\\macierzystego\\LogFiles\\aplikacji\\errors.txt rejestrowania w pliku hello na powitania został zwrócony wyjątek. Ten plik zawiera hello ślad stosu, można naprawić na podstawie tych aplikacji.
2. Aplikacja zużywa zbyt dużej ilości pamięci, co ma wpływ na inne procesy z wprowadzenie. Hello całkowitej ilości pamięci maszyny Wirtualnej w przypadku zamknięcia too100%, Twoje node.exe można kasować przez hello proces Menedżera toolet inne procesy pracę toodo szansy. toofix, upewnij się, że aplikacja nie jest przeciek pamięci albo jeśli użytkownik aplikacji musi naprawdę toouse dużej ilości pamięci, należy skalować tooa większych maszyn wirtualnych ze znacznie większą ilość pamięci RAM.

### <a name="my-node-application-does-not-start"></a>Moja aplikacja węzła nie uruchamia.
Jeśli aplikacja zwraca 500 błędów podczas uruchamiania, może istnieć kilka przyczyn:

1. Node.exe nie jest obecny w poprawnej lokalizacji hello. Sprawdź ustawienie nodeProcessCommandLine.
2. Plik skryptu głównego nie ma na powitania poprawnej lokalizacji. Plik web.config i upewnij się, że hello nazwę pliku głównego skryptu hello w pliku skryptu głównego hello dopasowań hello obsługi sekcji.
3. Plik Web.config konfiguracji jest niepoprawna — Sprawdź wartości nazwy ustawień hello.
4. Zimny Start — aplikacji trwa zbyt długo toostartup. Jeśli aplikacja będzie trwało dłużej niż (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1 000 sekund iisnode zwróci błąd 500. Zwiększenie wartości hello te toomatch ustawienia aplikacji uruchomić program iisnode tooprevent czasu z limit czasu i zwróci komunikat hello 500.

### <a name="my-node-application-crashed"></a>Moja aplikacja węzła awaria
Aplikacji wywołującej nieprzechwyconych wyjątków — d: wyboru Sprawdź\\macierzystego\\LogFiles\\aplikacji\\errors.txt rejestrowania w pliku hello na powitania został zwrócony wyjątek. Ten plik zawiera hello ślad stosu, można naprawić na podstawie tych aplikacji.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Moja aplikacja węzeł ma za dużo toostartup czasu (zimny Start)
Najczęstszą przyczyną tego jest aplikacji hello wiele plików w węźle hello\_moduły i tooload prób aplikacji hello większość tych plików podczas uruchamiania. Domyślnie ponieważ pliki znajdują się w udziale sieciowym hello na używanie Azure ładowanie tak wielu plików może zająć trochę czasu.
Niektóre toomake rozwiązania to szybciej są:

1. Upewnij się, że masz struktury płaskiej zależności i ma zduplikowane zależności za pomocą npm3 tooinstall własnych modułów.
2. Spróbuj obciążenia toolazy węzeł\_moduły i nie wszystkie moduły hello podczas uruchamiania obciążenia. Oznacza to, że toorequire('module') wywołania tej hello należy zrobić, jeśli potrzebujesz faktycznie w funkcji hello spróbuj toouse hello modułu.
3. Używanie Azure oferuje funkcję o nazwie lokalnej pamięci podręcznej. Ta funkcja kopiuje zawartość z hello sieci udziału toohello dysku lokalnego na powitania maszyny Wirtualnej. Ponieważ pliki hello są lokalne, hello czas węzła ładowania\_modułów jest znacznie szybsze. -Tym [dokumentacji](../app-service/app-service-local-cache.md) wyjaśniono, jak toouse lokalnej pamięci podręcznej w bardziej szczegółowo.

## <a name="iisnode-http-status-and-substatus"></a>Stan http IISNODE i podstanu
To [plik źródłowy](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) listy wszystkich iisnode kombinacja możliwe stan/podstanu hello może zwrócić w przypadku błędu.

Włącz FREB dla kod błędu win32 hello toosee aplikacji (Upewnij się, możesz włączyć FREB tylko w lokacjach nieprodukcyjnych ze względu na wydajność).

| Stan HTTP | Podstan protokołu HTTP | Możliwa przyczyna? |
| --- | --- | --- |
| 500 |1000 |Znaleziono niektórych problem podczas wysyłania tooIISNODE żądania hello — Sprawdź, czy node.exe został uruchomiony w. Node.exe może ulec awarii podczas uruchamiania. Sprawdź konfigurację web.config błędów. |
| 500 |1001 |-Win32Error 0x2 — aplikacja nie odpowiada toohello adresu URL. Ponowne zapisywanie adresów URL wyboru, reguł lub jeśli aplikacja express ma hello tras poprawne określonych. -Win32Error 0x6d — nazwany potok jest zajęty — Node.exe nie akceptuje żądania potoku hello jest zajęty. Sprawdź wysokiego użycia procesora cpu. -Inne błędy — Sprawdź, czy awaria node.exe. |
| 500 |1002 |Awaria node.exe — sprawdź d:\\macierzystego\\LogFiles\\rejestrowania errors.txt dla ślad stosu. |
| 500 |1003 |Konfiguracja potoku problem — powinien nigdy nie widzisz taki komunikat, ale jeśli to zrobisz, hello o nazwie Konfiguracja potoku jest nieprawidłowy. |
| 500 |1004-1018 |Wystąpił błąd podczas wysyłania odpowiedzi hello żądania lub przetwarzania hello z node.exe. Sprawdź, czy awaria node.exe. Sprawdź d:\\macierzystego\\LogFiles\\rejestrowania errors.txt dla ślad stosu. |
| 503 |1000 |Za mało pamięci tooallocate więcej o nazwie połączenia potoku. Sprawdź, dlaczego aplikacja zużywa dużej ilości pamięci. Sprawdź wartość ustawienia maxConcurrentRequestsPerProcess. Jeśli nie jest on nieskończone i wiele żądań, zwiększenie tej wartości tooprevent ten błąd. |
| 503 |1001 |Żądania nie można toonode.exe wysłane, ponieważ jest odtwarzanie aplikacji hello. Po aplikacji hello po odtworzeniu, żądania powinien być obsługiwany normalnie. |
| 503 |1002 |Kod błędu win32 wyboru przyczyny rzeczywiste — żądanie nie można node.exe tooa wysłane. |
| 503 |1003 |Nazwany potok jest zbyt zajęty — Sprawdź, czy węzeł zużywa dużo zasobów procesora |

Ustawienie w NODE.exe węzeł\_OCZEKUJE\_POTOKU\_WYSTĄPIEŃ. Domyślnie poza azure webapps ta wartość to 4. Oznacza to, że node.exe w czasie na powitania nazwany potok może akceptować tylko 4 żądania. Na używanie Azure too5000 tę wartość i wartość ta powinna być wystarczająca dla większości aplikacji węzła działających na używanie usługi azure. Użytkownik nie powinien być widoczny 503.1003 na używanie usługi azure, ponieważ będziemy mieć dużą wartość dla hello węzła\_OCZEKUJE\_POTOKU\_WYSTĄPIEŃ.  |

## <a name="more-resources"></a>Więcej zasobów
Wykonaj te toolearn łącza więcej informacji na temat aplikacji programu node.js w usłudze Azure App Service.

* [Rozpoczynanie pracy z aplikacjami sieci web Node.js w usłudze Azure App Service](app-service-web-get-started-nodejs.md)
* [Jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md)
* [Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps: Node.js (Aplikacje sieci Web w usłudze Azure App Service: Node.js)](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centrum deweloperów środowiska Node.js](../nodejs-use-node-modules-azure-apps.md)
* [Eksploracja hello Super Secret Kudu Debug konsoli](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

