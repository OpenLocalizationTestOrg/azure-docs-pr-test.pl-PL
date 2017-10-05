## <a name="build-iot-edge"></a><span data-ttu-id="a2297-101">Tworzenie krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="a2297-101">Build IoT Edge</span></span>

<span data-ttu-id="a2297-102">Ten samouczek używa niestandardowe moduły krawędzi IoT do komunikowania się ze zdalnym wstępnie skonfigurowane rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="a2297-102">This tutorial uses custom IoT Edge modules to communicate with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a2297-103">W związku z tym jest potrzebne do tworzenia krawędzi IoT modułów z kodu źródła niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="a2297-103">Therefore, you need to build the IoT Edge modules from custom source code.</span></span> <span data-ttu-id="a2297-104">W poniższych sekcjach opisano sposób instalowania krawędzi IoT i utworzenie niestandardowego modułu krawędzi IoT.</span><span class="sxs-lookup"><span data-stu-id="a2297-104">The following sections describe how to install IoT Edge and build the custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="a2297-105">Zainstaluj krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="a2297-105">Install IoT Edge</span></span>

<span data-ttu-id="a2297-106">W poniższych krokach opisano sposób instalowania oprogramowania wstępnie skompilowanym krawędzi IoT na Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="a2297-106">The following steps describe how to install the pre-compiled IoT Edge software on the Intel NUC:</span></span>

1. <span data-ttu-id="a2297-107">Skonfiguruj repozytoria wymagany pakiet inteligentne, uruchamiając następujące polecenia na Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="a2297-107">Configure the required smart package repositories by running the following commands on the Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="a2297-108">Wprowadź `y` gdy pojawi się monit o polecenie **obejmują ten kanał?**.</span><span class="sxs-lookup"><span data-stu-id="a2297-108">Enter `y` when the command prompts you to **Include this channel?**.</span></span>

1. <span data-ttu-id="a2297-109">Aktualizacja Menedżera pakietów inteligentne, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a2297-109">Update the smart package manager by running the following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="a2297-110">Zainstaluj pakiet Azure IoT krawędzi, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a2297-110">Install the Azure IoT Edge package by running the following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="a2297-111">Weryfikowanie instalacji przez uruchomienie przykładu "Hello world".</span><span class="sxs-lookup"><span data-stu-id="a2297-111">Verify the installation by running the "Hello world" sample.</span></span> <span data-ttu-id="a2297-112">W tym przykładzie zapisuje wiadomość hello world pliku log.txT co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="a2297-112">This sample writes a hello world message to the log.txT file every five seconds.</span></span> <span data-ttu-id="a2297-113">Poniższe polecenia są uruchamiane przykładu "Hello world":</span><span class="sxs-lookup"><span data-stu-id="a2297-113">The following commands run the "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="a2297-114">Ignoruj wszystkie **nieprawidłowy argument** wiadomości po zatrzymaniu próbki.</span><span class="sxs-lookup"><span data-stu-id="a2297-114">Ignore any **invalid argument** messages when you stop the sample.</span></span>

    <span data-ttu-id="a2297-115">Aby wyświetlić zawartość pliku dziennika, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a2297-115">Use the following command to view the contents of the log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="a2297-116">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="a2297-116">Troubleshooting</span></span>

<span data-ttu-id="a2297-117">Jeśli zostanie wyświetlony błąd "nie zawiera util-linux deweloperów", spróbuj wykonać ponowny rozruch Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a2297-117">If you receive the error "No package provides util-linux-dev", try rebooting the Intel NUC.</span></span>
