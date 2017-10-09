### <a name="create-a-nodejs-application"></a>Tworzenie aplikacji w języku Node.js

Utwórz plik JavaScript o nazwie `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Dodaj pakiet NPM przekazywania hello

Uruchom polecenie `npm install hyco-ws` w wierszu polecenia języka Node w folderze projektu.

### <a name="write-some-code-toosend-messages"></a>Napisanie kodu toosend wiadomości

1. Dodaj następujące hello `constants` toohello początku hello `sender.js` pliku.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Dodaj następujące toohello stałe hello `sender.js` szczegóły połączenia hybrydowe hello w pliku. Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.
   
   1. `const ns`-hello przekazywania przestrzeni nazw. Czy toouse hello przestrzeni nazw w pełni kwalifikowana nazwa; na przykład `{namespace}.servicebus.windows.net`.
   2. `const path`-Nazwa hello hello połączenia hybrydowego.
   3. `const keyrule`-hello nazwa klucza SAS hello.
   4. `const key`-hello wartości klucza sygnatury dostępu Współdzielonego.

3. Dodaj hello następującego kodu toohello `sender.js` pliku:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Oto jak powinien wyglądać plik sender.js:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

