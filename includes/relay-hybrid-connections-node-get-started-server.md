### <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js

Utwórz plik JavaScript o nazwie `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Dodaj pakiet NPM przekazywania hello

Uruchom polecenie `npm install hyco-ws` w wierszu polecenia języka Node w folderze projektu.

### <a name="write-some-code-tooreceive-messages"></a>Napisanie kodu tooreceive wiadomości

1. Dodaj powitania od góry stałej toohello hello `listener.js` pliku.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Dodaj następujące toohello stałe hello `listener.js` szczegóły połączenia hybrydowe hello w pliku. Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.
   
   1. `const ns`-hello przekazywania przestrzeni nazw. Czy toouse hello przestrzeni nazw w pełni kwalifikowana nazwa; na przykład `{namespace}.servicebus.windows.net`.
   2. `const path`-Nazwa hello hello połączenia hybrydowego.
   3. `const keyrule`-hello nazwa klucza SAS hello.
   4. `const key`-hello wartości klucza sygnatury dostępu Współdzielonego.

3. Dodaj hello następującego kodu toohello `listener.js` pliku:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Plik listener.js powinien wyglądać w następujący sposób:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

