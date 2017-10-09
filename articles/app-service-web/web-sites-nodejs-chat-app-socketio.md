---
title: "aaaCreate aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze Azure App Service"
description: "Samouczek przedstawiający przy użyciu biblioteki socket.io w użyciu w aplikacji sieci web node.js hostowanej na platformie Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usłudze Azure App Service
Użyciu biblioteki Socket.IO udostępnia w czasie rzeczywistym komunikacji między serwerem środowiska node.js i klientów przy użyciu protokołu WebSockets. Obsługuje ona również transportów tooother rezerwowy (na przykład długiego sondowania) współdziałających ze starszych przeglądarek. Ten samouczek przeprowadzi użytkownika przez proces hostingu użyciu biblioteki Socket.IO na podstawie rozmów aplikacji jako aplikacji sieci web platformy Azure, a pokazują, jak tooscale hello aplikacji przy użyciu [pamięć podręczna Redis Azure]. Aby uzyskać więcej informacji o użyciu biblioteki Socket.IO, zobacz <http://socket.io/>.

> [!NOTE]
> Hello procedur w tym zadaniu zastosować zbyt[aplikacji usługi sieci Web aplikacji]; dla usługi w chmurze, zobacz [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Pobierz przykład Witaj rozmowy
Dla tego projektu, użyjemy przykład Witaj rozmów z hello [repozytorium GitHub użyciu biblioteki Socket.IO]. Wykonaj poniższy przykład hello toodownload kroki hello i dodaj go projektu toohello, utworzonych wcześniej.

1. Pobierz [ZIP lub GZ zarchiwizowane wersji] hello użyciu biblioteki Socket.IO projektu (wersja 1.3.5 zostało użyte dla tego dokumentu)
2. Wyodrębnij hello archiwum i skopiuj hello **przykłady\\rozmów** katalogu tooa nowej lokalizacji. Na przykład  **\\węzła\\rozmów**.

## <a name="modify-appjs-and-install-modules"></a>Modyfikowanie pliku app.js i zainstalować moduły
1. Zmień nazwę hello **index.js** pliku zbyt**app.js**. Dzięki temu Azure toodetect, że jest to aplikacji Node.js.
2. Otwórz hello **app.js** plik w edytorze tekstów. Zmień hello wiersz zawierający `var io = require('../..')(server);` w sposób przedstawiony poniżej:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Otwórz hello **package.json** plik i dodać toosocket.io odwołania, w obszarze `dependencies`, jak pokazano poniżej:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Z wiersza polecenia hello, zmień toohello  **\\węzła\\rozmów** katalogu i użyj tooinstall hello moduły npm wymagane przez tę aplikację:
   
        npm install
   
    Spowoduje to zainstalowanie modułów hello do podfolderu o nazwie **node_modules**.

## <a name="create-an-azure-web-app"></a>Tworzenie aplikacji sieci Web platformy Azure
Wykonaj te kroki toocreate aplikacji sieci web platformy Azure, włączyć publikowanie w usłudze Git, a następnie włącz obsługę protokołu WebSocket dla aplikacji sieci web hello.

> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.
> 
> 

1. Zainstaluj hello interfejsu wiersza polecenia platformy Azure (Azure CLI), a następnie połącz tooyour subskrypcji platformy Azure. Zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).
2. Jeśli jest to pierwszy ustawienia czasu zapasowej repozytorium na platformie Azure, należy toocreate poświadczenia logowania. Z hello Azure CLI wprowadź następujące polecenie hello:
   
        azure site deployment user set [username] [password]
3. Zmień toohello  **\\node\chat** katalogu i użyj hello następujące polecenia toocreate nowej aplikacji sieci web platformy Azure i lokalnego repozytorium Git. To polecenie tworzy również Git zdalnego o nazwie "azure".
   
        azure site create mysitename --git
   
    "Mysitename" należy zamienić na unikatową nazwę aplikacji sieci web.
4. Zatwierdź hello istniejące pliki toohello lokalnego repozytorium przy użyciu hello następującego polecenia:
   
        git add .
        git commit -m "Initial commit"
5. Wypchnij repozytorium Azure Web Apps toohello pliki hello za pomocą hello następujące polecenie:
   
        git push azure master
   
    Po wyświetleniu monitu wprowadź swoje poświadczenia w kroku 2. Komunikaty o stanie zostanie wyświetlony jako moduły są importowane na powitania serwera. Po zakończeniu tego procesu aplikacji hello będzie udostępniana w aplikacji sieci web platformy Azure.
   
   > [!NOTE]
   > Podczas instalacji modułu mogą pojawić się błędy który "hello... zaimportowanego projektu nie został znaleziony '. Te można bezpiecznie zignorować.
   > 
   > 
6. Użyciu biblioteki Socket.IO używa protokołu Websocket, które nie są włączone domyślnie na platformie Azure. tooenable gniazda sieci web, należy użyć następującego polecenia hello:
   
        azure site set -w
   
    Jeśli zostanie wyświetlony monit, wprowadź nazwę hello hello aplikacji sieci web.
   
   > [!NOTE]
   > Witaj "set -w witrynie azure" zostanie polecenie pracować tylko z wersji 0.7.4 lub nowszej hello interfejsu wiersza polecenia platformy Azure. Można również włączyć obsługę protokołu WebSocket przy użyciu hello [Azure Portal](https://portal.azure.com).
   > 
   > przy użyciu protokołu WebSockets tooenable hello portalu Azure kliknij hello aplikacji sieci web z hello blok aplikacje sieci Web, kliknij przycisk **wszystkie ustawienia** > **ustawienia aplikacji**. W obszarze **gniazda sieci Web**, kliknij przycisk **na**. Następnie kliknij przycisk **Save** (Zapisz).
   > 
   > 
7. aplikacji sieci web hello tooview po hello w usłudze Azure, użyj polecenia toolaunch przeglądarki sieci web i przejdź toohello hostowanych aplikacji sieci web:
   
        azure site browse

Aplikacja jest teraz uruchomiona na platformie Azure i możliwość przekazywania wiadomości między różnych klientów przy użyciu użyciu biblioteki Socket.IO.

## <a name="scale-out"></a>Skalowanie w poziomie
Użyciu biblioteki Socket.IO aplikacji może być skalowana w poziomie za pomocą **karty** toodistribute wiadomości i zdarzenia między wiele wystąpień aplikacji. Mimo że dostępnych jest kilka kart, hello [redis użyciu biblioteki socket.io] karty mogą być łatwo używane z funkcją pamięć podręczna Redis Azure hello.

> [!NOTE]
> Dodatkowe wymagania dla skalowania rozwiązania użyciu biblioteki Socket.IO jest obsługa trwałe sesje. Trwałe sesje są domyślnie włączone dla aplikacji sieci Web platformy Azure za pośrednictwem Routing żądań Azure. Aby uzyskać więcej informacji, zobacz [wystąpienia koligacji w Azure Web Sites].
> 
> 

### <a name="create-a-redis-cache"></a>Tworzenie pamięci podręcznej Redis
Wykonaj kroki opisane hello w [tworzenia pamięci podręcznej w pamięci podręcznej Redis Azure] toocreate nowej pamięci podręcznej.

> [!NOTE]
> Zapisz hello **nazwy hosta** i **klucz podstawowy** dla pamięci podręcznej, ponieważ będą one potrzebne w hello następnych kroków.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Dodaj hello redis i użyciu biblioteki socket.io redis modułów
1. W wierszu polecenia Zmień toohello  **\\węzła\\rozmów** hello katalogu i użyj następującego polecenia.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > wersje Hello określone w tym poleceniu są używane podczas testowania w tym artykule wersje hello.
   > 
   > 
2. Modyfikowanie hello **app.js** pliku tooadd hello następujące wiersze natychmiast po`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Zastąp **redishostname** i **rediskey** z nazwą hosta hello i klucza pamięci podręcznej Redis.
   
    Spowoduje to utworzenie Publikuj i Subskrybuj toohello klienta pamięci podręcznej Redis utworzone wcześniej. Klienci Hello są następnie używane z tooconfigure karty hello hello toouse użyciu biblioteki Socket.IO pamięć podręczna Redis do przekazywania wiadomości i zdarzenia między wystąpieniami aplikacji
   
   > [!NOTE]
   > Podczas hello **redis użyciu biblioteki socket.io** karty może komunikować się bezpośrednio tooRedis, hello bieżąca wersja nie obsługuje uwierzytelniania hello wymagane przez pamięci podręcznej Azure Redis. Dlatego połączenia początkowego hello jest tworzony przy użyciu hello **redis** modułu, następnie powitania klienta jest przekazywany toohello **redis użyciu biblioteki socket.io** karty.
   > 
   > Pamięć podręczna Redis Azure obsługuje bezpiecznych połączeń przy użyciu portu 6380, moduły hello używane w tym przykładzie nie obsługują bezpiecznych połączeń wersji 2014-7-14. Hello powyżej kod używa hello domyślnie niezabezpieczone port 6379.
   > 
   > 
3. Witaj Zapisz zmodyfikowany **app.js**

### <a name="commit-changes-and-redeploy"></a>Zatwierdź zmiany i ponownie wdrożyć
Z wiersza polecenia w hello hello  **\\węzła\\rozmów** katalogu, użyj hello następujące zmiany toocommit poleceń i wdrożenie aplikacji hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Po hello zmiany mają został naciśnięty toohello serwera, witryny można skalować w wielu wystąpieniach za pomocą następującego polecenia hello.

    azure site scale instances --instances #

Gdzie  **#**  hello liczbę wystąpień toocreate.

Aplikacja sieci web tooyour można połączyć z wielu tooverify przeglądarki lub komputery, które są prawidłowo wysyłane tooall klientów.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="connection-limits"></a>Limity połączeń
Aplikacje sieci Web platformy Azure są dostępne w wielu jednostki magazynowe, które określają hello zasoby dostępne tooyour lokacji. W tym hello liczbę dozwolonych połączeń protokołu WebSocket. Aby uzyskać więcej informacji, zobacz hello [stronie cennika usługi sieci Web Apps].

### <a name="messages-arent-being-sent-using-websockets"></a>Komunikaty nie są wysyłane przy użyciu protokołu WebSockets
Jeśli przeglądarka klienta zachować nastąpi powrót toolong sondowania zamiast Websocket, może być ze względu na jedną z następujących hello.

* **Spróbuj ograniczyć hello transportu toojust WebSockets**
  
    Aby toouse użyciu biblioteki Socket.IO Websocket jako hello transportu do obsługi komunikatów zarówno powitania serwera i klienta muszą obsługiwać protokół WebSockets. Jeśli co najmniej hello innych nie, użyciu biblioteki Socket.IO będzie negocjował innego transportu, takich jak długiego sondowania. Witaj domyślna lista transportów używany przy użyciu biblioteki Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`. Aby wymusić użycie tooonly Websocket przez dodanie powitania po toohello kodu **app.js** pliku po hello wiersz zawierający `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Należy pamiętać, że starszych przeglądarek, które nie obsługują protokół WebSockets nie będą mogli tooconnect toohello lokacji podczas hello powyżej kodu jest aktywny, ponieważ ogranicza komunikację tooWebSockets tylko.
  > 
  > 
* **Użyj protokołu SSL**
  
    Protokół WebSockets opiera się na niektórych mniejszym używane nagłówków HTTP, takie jak hello **uaktualnienia** nagłówka. Niektóre urządzenia sieci pośredniczącej, takich jak serwer proxy sieci web, może spowodować usunięcie tych nagłówków. tooavoid ten problem, można ustanowić połączenia obiektu WebSocket hello za pośrednictwem protokołu SSL.
  
    Tooaccomplish łatwo jest zbyt tooconfigure użyciu biblioteki Socket.IO`match origin protocol`. To powoduje, że użyciu biblioteki Socket.IO toosecure Websocket komunikacji hello identyczny hello pochodzących HTTP/HTTPS Żądanie hello strony sieci web. Jeśli przeglądarka używa toovisit adres HTTPS URL witryny sieci Web, kolejne komunikacji protokołu WebSocket za pośrednictwem użyciu biblioteki Socket.IO będą chronione za pośrednictwem protokołu SSL.
  
    toomodify tooenable w tym przykładzie tę konfigurację, Dodaj hello następującego kodu toohello **app.js** plik po hello wiersz zawierający `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Sprawdź ustawienia pliku web.config**
  
    Aplikacje sieci web platformy Azure, które obsługę aplikacji programu Node.js Użyj hello **web.config** tooroute plików przychodzących żądań toohello aplikacji Node.js. Dla toofunction Websocket poprawnie z aplikacji programu Node.js, hello **web.config** musi zawierać hello wejścia.
  
        <webSocket enabled="false"/>
  
    Powoduje wyłączenie hello moduł Websocket usług IIS, który zawiera własną implementację Websocket i powoduje konflikt z Node.js określone moduły protokołu WebSocket, takich jak użyciu biblioteki Socket.IO. Jeśli ten wiersz nie jest obecny lub jest zbyt`true`, może to być powód hello hello transportu protokołu WebSocket nie działa dla aplikacji.
  
    Zwykle nie dołączaj aplikacji Node.js **web.config** pliku, więc witryn sieci Web Azure automatycznie generuje jeden dla aplikacji programu Node.js podczas ich wdrażania. Ponieważ ten plik jest automatycznie generowany na powitania serwera, należy użyć hello FTP i FTPS adres URL dla Twojej witryny sieci Web tooview tego pliku. Znajdowanie hello FTP i FTPS adres URL witryny w portalu klasycznym hello przez wybranie aplikacji sieci web i następnie hello **pulpitu nawigacyjnego** łącza. Witaj adresy URL są wyświetlane w hello **szybkiego dostępu** sekcji.
  
  > [!NOTE]
  > Witaj **web.config** pliku tylko jest generowany przez usługę Azure Websites, jeśli aplikacja nie zapewnia. Jeśli podasz **web.config** pliku w katalogu głównym hello projektu aplikacji, będzie używany przez aplikacje sieci Web Azure.
  > 
  > 
  
    Hello wpis nie jest obecny, czy ustawiono wartość tooa `true`, a następnie należy utworzyć **web.config** w hello katalogu głównego aplikacji Node.js i określ wartość `false`.  Odwołania, poniżej hello jest domyślnie **web.config** dla aplikacji, która używa **app.js** jako punkt wejścia hello.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Jeśli aplikacja używa innej niż punkt wejścia **app.js**, musisz zastąpić wszystkie wystąpienia **app.js** z hello Popraw punktu wejścia. Na przykład, zastępując **app.js** z **server.js**.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service], gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób toocreate aplikacji czatu hostowanej w aplikacji sieci web platformy Azure. Może również obsługiwać tę aplikację jako usługi w chmurze platformy Azure. Instrukcje na temat tooaccomplish tego, zobacz [tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure].

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js].

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure].

<!-- URL List -->

[pamięć podręczna Redis Azure]: /documentation/services/redis-cache/
[aplikacji usługi sieci Web aplikacji]: http://go.microsoft.com/fwlink/?LinkId=529714
[stronie cennika usługi sieci Web Apps]: http://go.microsoft.com/fwlink/?LinkId=511643
[tworzenie aplikacji czatu Node.js przy użyciu biblioteki Socket.IO w usługi w chmurze platformy Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centrum deweloperów środowiska Node.js]: /develop/nodejs/
[Wypróbuj usługę App Service]: https://azure.microsoft.com/try/app-service/
[wystąpienia koligacji w Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[tworzenia pamięci podręcznej w pamięci podręcznej Redis Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[redis użyciu biblioteki socket.io]: https://github.com/socketio/socket.io-redis
[repozytorium GitHub użyciu biblioteki Socket.IO]: https://github.com/socketio/socket.io
[ZIP lub GZ zarchiwizowane wersji]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
