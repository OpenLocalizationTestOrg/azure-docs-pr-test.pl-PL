## <a name="configure-the-nodejs-simulated-device"></a><span data-ttu-id="78645-101">Konfigurowanie środowiska Node.js symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="78645-101">Configure the Node.js simulated device</span></span>
1. <span data-ttu-id="78645-102">Na pulpicie nawigacyjnym monitorowania zdalnego kliknij **+ Dodaj urządzenie** , a następnie dodaj *urządzeń niestandardowych*.</span><span class="sxs-lookup"><span data-stu-id="78645-102">On the remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="78645-103">Zanotuj Centrum IoT nazwy hosta, identyfikator urządzenia i klucz urządzenia.</span><span class="sxs-lookup"><span data-stu-id="78645-103">Make a note of the IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="78645-104">Należy je później w tym samouczku podczas przygotowywania remote_monitoring.js aplikację klienta dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="78645-104">You need them later in this tutorial when you prepare the remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="78645-105">Upewnij się, że wersji środowiska Node.js 0.12.x lub nowszy jest zainstalowany na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="78645-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="78645-106">Uruchom `node --version` w wierszu polecenia lub w powłoce, aby sprawdzić wersję.</span><span class="sxs-lookup"><span data-stu-id="78645-106">Run `node --version` at a command prompt or in a shell to check the version.</span></span> <span data-ttu-id="78645-107">Aby uzyskać informacje dotyczące instalowania programu Node.js w systemie Linux przy użyciu Menedżera pakietów, zobacz [instalowanie Node.js za pomocą Menedżera pakietów][node-linux].</span><span class="sxs-lookup"><span data-stu-id="78645-107">For information about using a package manager to install Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="78645-108">Po zainstalowaniu programu Node.js w klonowania najnowszą wersję [azure iot-sdk węzłami] [ lnk-github-repo] repozytorium na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="78645-108">When you have installed Node.js, clone the latest version of the [azure-iot-sdk-node][lnk-github-repo] repository to your development machine.</span></span> <span data-ttu-id="78645-109">Zawsze używaj **wzorca** gałęzi do najnowszej wersji biblioteki i przykłady.</span><span class="sxs-lookup"><span data-stu-id="78645-109">Always use the **master** branch for the latest version of the libraries and samples.</span></span>
4. <span data-ttu-id="78645-110">Z lokalną kopię [azure iot-sdk węzłami] [ lnk-github-repo] repozytorium, pliki kopii dwa z folderu węzła/urządzenia/próbek do pustego folderu na komputerze deweloperskim:</span><span class="sxs-lookup"><span data-stu-id="78645-110">From your local copy of the [azure-iot-sdk-node][lnk-github-repo] repository, copy the following two files from the node/device/samples folder to an empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="78645-111">Packages.JSON</span><span class="sxs-lookup"><span data-stu-id="78645-111">packages.json</span></span>
   * <span data-ttu-id="78645-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="78645-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="78645-113">Otwórz plik remote_monitoring.js i poszukaj następujących definicji zmiennej:</span><span class="sxs-lookup"><span data-stu-id="78645-113">Open the remote_monitoring.js file and look for the following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="78645-114">Zastąp **[parametry połączenia Centrum IoT urządzenia]** z parametrów połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="78645-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="78645-115">Użyj wartości dla nazwy hosta Centrum IoT, identyfikator urządzenia i klucz urządzenia, który należy zanotować w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="78645-115">Use the values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="78645-116">Ciąg połączenia urządzenia ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="78645-116">A device connection string has the following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="78645-117">Jeśli nazwa hosta z Centrum IoT jest **contoso** i identyfikator urządzenia jest **mydevice**, ciąg połączenia prawdopodobnie następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="78645-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like the following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Zapisz plik. <span data-ttu-id="78645-119">Uruchom następujące polecenia w powłoce lub wiersza polecenia w folderze, który zawiera te pliki, aby zainstalować wymagane pakiety, a następnie uruchom przykładową aplikację:</span><span class="sxs-lookup"><span data-stu-id="78645-119">Run the following commands in a shell or command prompt in the folder that contains these files to install the necessary packages and then run the sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="78645-120">Obserwować dynamiczne telemetrii w akcji</span><span class="sxs-lookup"><span data-stu-id="78645-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="78645-121">Pulpitu nawigacyjnego przedstawia dane telemetryczne temperatury i wilgotności z istniejących urządzeń symulowanego:</span><span class="sxs-lookup"><span data-stu-id="78645-121">The dashboard shows the temperature and humidity telemetry from the existing simulated devices:</span></span>

![Domyślny pulpit nawigacyjny][image1]

<span data-ttu-id="78645-123">W przypadku wybrania symulowane urządzenie Node.js, który działał w poprzedniej sekcji, zobacz temperatury, wilgotności i dane telemetryczne temperatury zewnętrznych:</span><span class="sxs-lookup"><span data-stu-id="78645-123">If you select the Node.js simulated device you ran in the previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![Dodaj zewnętrzne temperatury do pulpitu nawigacyjnego][image2]

<span data-ttu-id="78645-125">Rozwiązanie monitorowania zdalnego automatycznie wykrywa typ telemetrii dodatkowe temperatury zewnętrznych i dodaje go do wykresu w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="78645-125">The remote monitoring solution automatically detects the additional external temperature telemetry type and adds it to the chart on the dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png