### <a name="create-a-nodejs-application"></a><span data-ttu-id="e0744-101">Tworzenie aplikacji w języku Node.js</span><span class="sxs-lookup"><span data-stu-id="e0744-101">Create a Node.js application</span></span>

<span data-ttu-id="e0744-102">Utwórz plik JavaScript o nazwie `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="e0744-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="e0744-103">Dodawanie pakietu NPM usługi Relay</span><span class="sxs-lookup"><span data-stu-id="e0744-103">Add the Relay NPM package</span></span>

<span data-ttu-id="e0744-104">Uruchom polecenie `npm install hyco-ws` w wierszu polecenia języka Node w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="e0744-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="e0744-105">Pisanie kodu w celu wysyłania komunikatów</span><span class="sxs-lookup"><span data-stu-id="e0744-105">Write some code to send messages</span></span>

1. <span data-ttu-id="e0744-106">Dodaj następujący element `constants` na początku pliku `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="e0744-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="e0744-107">Dodaj następujące stałe do pliku `sender.js` na potrzeby szczegółów połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="e0744-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="e0744-108">Zastąp symbole zastępcze w nawiasach wartościami uzyskanymi podczas tworzenia połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="e0744-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="e0744-109">`const ns` — obszar nazw usługi Relay.</span><span class="sxs-lookup"><span data-stu-id="e0744-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="e0744-110">Pamiętaj, aby użyć w pełni kwalifikowanej nazwy obszaru nazw, na przykład `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e0744-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="e0744-111">`const path` — nazwa połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="e0744-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="e0744-112">`const keyrule` — nazwa klucza sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e0744-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="e0744-113">`const key` — wartość klucza sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e0744-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="e0744-114">Dodaj następujący kod do pliku `sender.js`:</span><span class="sxs-lookup"><span data-stu-id="e0744-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="e0744-115">Oto jak powinien wyglądać plik sender.js:</span><span class="sxs-lookup"><span data-stu-id="e0744-115">Here is what your sender.js file should look like:</span></span>
   
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

