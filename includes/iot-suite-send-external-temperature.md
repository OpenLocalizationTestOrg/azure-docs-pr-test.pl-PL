## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="9481d-101">Skonfiguruj hello Node.js symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="9481d-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="9481d-102">Na powitania zdalnego pulpitu nawigacyjnego monitorowania, kliknij przycisk **+ Dodaj urządzenie** , a następnie dodaj *urządzeń niestandardowych*.</span><span class="sxs-lookup"><span data-stu-id="9481d-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="9481d-103">Zanotuj hello Centrum IoT nazwy hosta, identyfikator urządzenia i klucz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9481d-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="9481d-104">Należy je później w tym samouczku podczas przygotowywania hello remote_monitoring.js urządzenia klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9481d-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="9481d-105">Upewnij się, że wersji środowiska Node.js 0.12.x lub nowszy jest zainstalowany na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="9481d-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="9481d-106">Uruchom `node --version` w wierszu polecenia lub w wersji hello toocheck powłoki.</span><span class="sxs-lookup"><span data-stu-id="9481d-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="9481d-107">Aby dowiedzieć się, jak za pomocą pakietu Menedżera tooinstall Node.js w systemie Linux, zobacz [instalowanie Node.js za pomocą Menedżera pakietów][node-linux].</span><span class="sxs-lookup"><span data-stu-id="9481d-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="9481d-108">Po zainstalowaniu programu Node.js w klonowania hello najnowszą wersję hello [azure iot-sdk węzłami] [ lnk-github-repo] komputerze deweloperskim tooyour repozytorium.</span><span class="sxs-lookup"><span data-stu-id="9481d-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="9481d-109">Zawsze używaj hello **wzorca** gałęzi do najnowszej wersji hello hello bibliotek i przykładów.</span><span class="sxs-lookup"><span data-stu-id="9481d-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="9481d-110">Z kopii lokalnej hello [azure iot-sdk węzłami] [ lnk-github-repo] repozytorium, hello kopiowania następujące dwa pliki z hello węzła/urządzenia/przykłady tooan pustego folderu na komputerze deweloperskim:</span><span class="sxs-lookup"><span data-stu-id="9481d-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="9481d-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="9481d-111">packages.json</span></span>
   * <span data-ttu-id="9481d-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="9481d-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="9481d-113">Otwórz plik remote_monitoring.js hello i wyszukaj powitania po definicji zmiennej:</span><span class="sxs-lookup"><span data-stu-id="9481d-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="9481d-114">Zastąp **[parametry połączenia Centrum IoT urządzenia]** z parametrów połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9481d-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="9481d-115">Użyj hello wartości dla nazwy hosta Centrum IoT, identyfikator urządzenia i klucz urządzenia, który należy zanotować w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="9481d-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="9481d-116">Ciąg połączenia urządzenia ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="9481d-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="9481d-117">Jeśli nazwa hosta z Centrum IoT jest **contoso** i identyfikator urządzenia jest **mydevice**, ciąg połączenia prawdopodobnie hello następującego fragmentu:</span><span class="sxs-lookup"><span data-stu-id="9481d-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Zapisz plik hello. <span data-ttu-id="9481d-119">Uruchom następujące polecenia w powłoce lub wiersza polecenia w folderze hello, który zawiera te pliki tooinstall hello niezbędne pakiety hello, a następnie uruchom hello przykładowej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="9481d-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="9481d-120">Obserwować dynamiczne telemetrii w akcji</span><span class="sxs-lookup"><span data-stu-id="9481d-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="9481d-121">pulpit nawigacyjny Hello zawiera hello temperatury i wilgotności dane telemetryczne z istniejących urządzeń symulowane hello:</span><span class="sxs-lookup"><span data-stu-id="9481d-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![Witaj domyślnego pulpitu nawigacyjnego][image1]

<span data-ttu-id="9481d-123">W przypadku wybrania hello Node.js symulowane urządzenie uruchomienia w poprzedniej sekcji hello Zobacz temperatury, wilgotności i dane telemetryczne temperatury zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="9481d-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Dodaj pulpit nawigacyjny toohello temperatury zewnętrznych][image2]

<span data-ttu-id="9481d-125">rozwiązanie monitorowania zdalnego Hello automatycznie wykrywa typ telemetrii dodatkowe temperatury zewnętrznych hello i dodaje go wykresu toohello na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9481d-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png