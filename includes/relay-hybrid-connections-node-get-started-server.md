### <a name="create-a-nodejs-application"></a><span data-ttu-id="d1542-101">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="d1542-101">Create a Node.js application</span></span>

<span data-ttu-id="d1542-102">Utwórz plik JavaScript o nazwie `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="d1542-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="d1542-103">Dodaj pakiet NPM przekazywania hello</span><span class="sxs-lookup"><span data-stu-id="d1542-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="d1542-104">Uruchom polecenie `npm install hyco-ws` w wierszu polecenia języka Node w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="d1542-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="d1542-105">Napisanie kodu tooreceive wiadomości</span><span class="sxs-lookup"><span data-stu-id="d1542-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="d1542-106">Dodaj powitania od góry stałej toohello hello `listener.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="d1542-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="d1542-107">Dodaj następujące toohello stałe hello `listener.js` szczegóły połączenia hybrydowe hello w pliku.</span><span class="sxs-lookup"><span data-stu-id="d1542-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="d1542-108">Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="d1542-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="d1542-109">`const ns`-hello przekazywania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d1542-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="d1542-110">Czy toouse hello przestrzeni nazw w pełni kwalifikowana nazwa; na przykład `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="d1542-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="d1542-111">`const path`-Nazwa hello hello połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="d1542-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="d1542-112">`const keyrule`-hello nazwa klucza SAS hello.</span><span class="sxs-lookup"><span data-stu-id="d1542-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="d1542-113">`const key`-hello wartości klucza sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d1542-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="d1542-114">Dodaj hello następującego kodu toohello `listener.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="d1542-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="d1542-115">Plik listener.js powinien wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1542-115">Here is what your listener.js file should look like:</span></span>
   
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

