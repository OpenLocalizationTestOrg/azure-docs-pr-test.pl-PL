### <a name="create-a-nodejs-application"></a><span data-ttu-id="c66b9-101">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="c66b9-101">Create a Node.js application</span></span>

<span data-ttu-id="c66b9-102">Utwórz plik JavaScript o nazwie `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="c66b9-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="c66b9-103">Dodaj pakiet NPM przekazywania hello</span><span class="sxs-lookup"><span data-stu-id="c66b9-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="c66b9-104">Uruchom polecenie `npm install hyco-ws` w wierszu polecenia języka Node w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="c66b9-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="c66b9-105">Napisanie kodu toosend wiadomości</span><span class="sxs-lookup"><span data-stu-id="c66b9-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="c66b9-106">Dodaj następujące hello `constants` toohello początku hello `sender.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="c66b9-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="c66b9-107">Dodaj następujące toohello stałe hello `sender.js` szczegóły połączenia hybrydowe hello w pliku.</span><span class="sxs-lookup"><span data-stu-id="c66b9-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="c66b9-108">Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="c66b9-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="c66b9-109">`const ns`-hello przekazywania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c66b9-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="c66b9-110">Czy toouse hello przestrzeni nazw w pełni kwalifikowana nazwa; na przykład `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c66b9-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="c66b9-111">`const path`-Nazwa hello hello połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="c66b9-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="c66b9-112">`const keyrule`-hello nazwa klucza SAS hello.</span><span class="sxs-lookup"><span data-stu-id="c66b9-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="c66b9-113">`const key`-hello wartości klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="c66b9-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="c66b9-114">Dodaj hello następującego kodu toohello `sender.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="c66b9-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="c66b9-115">Oto jak powinien wyglądać plik sender.js:</span><span class="sxs-lookup"><span data-stu-id="c66b9-115">Here is what your sender.js file should look like:</span></span>
   
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

