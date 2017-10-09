## <a name="build-iot-edge"></a><span data-ttu-id="5140d-101">Tworzenie krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="5140d-101">Build IoT Edge</span></span>

<span data-ttu-id="5140d-102">W tym samouczku używa niestandardowych toocommunicate modułów krawędzi IoT z hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5140d-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="5140d-103">W związku z tym należy toobuild hello krawędzi IoT modułów z kodu źródła niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="5140d-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="5140d-104">Hello następujące sekcje opisują sposób tooinstall krawędzi IoT i kompilacji hello niestandardowego modułu IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="5140d-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="5140d-105">Zainstaluj krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="5140d-105">Install IoT Edge</span></span>

<span data-ttu-id="5140d-106">Witaj poniższych krokach opisano sposób tooinstall hello wstępnie skompilowany oprogramowanie krawędzi IoT na powitania Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="5140d-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="5140d-107">Skonfiguruj repozytoriów pakietu inteligentne hello wymagane, uruchamiając następujące polecenia na powitania Intel NUC hello:</span><span class="sxs-lookup"><span data-stu-id="5140d-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="5140d-108">Wprowadź `y` po hello polecenie monituje zbyt**obejmują ten kanał?**.</span><span class="sxs-lookup"><span data-stu-id="5140d-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="5140d-109">Aktualizacja Menedżera pakietów inteligentne hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="5140d-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="5140d-110">Zainstaluj pakiet Azure IoT krawędzi hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="5140d-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="5140d-111">Sprawdź instalacji hello uruchomionych powitania "Hello world" przykładowe.</span><span class="sxs-lookup"><span data-stu-id="5140d-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="5140d-112">W tym przykładzie zapisuje plik log.txT toohello wiadomość hello world co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="5140d-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="5140d-113">Witaj następujące polecenia Uruchom powitania "Hello world" próbki:</span><span class="sxs-lookup"><span data-stu-id="5140d-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="5140d-114">Ignoruj wszystkie **nieprawidłowy argument** wiadomości po zatrzymaniu hello próbki.</span><span class="sxs-lookup"><span data-stu-id="5140d-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="5140d-115">Użyj następującego polecenia tooview hello zawartość pliku dziennika hello hello:</span><span class="sxs-lookup"><span data-stu-id="5140d-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="5140d-116">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="5140d-116">Troubleshooting</span></span>

<span data-ttu-id="5140d-117">Jeśli wystąpi błąd hello "pakiet nie zawiera util-linux deweloperów", spróbuj wykonać ponowny rozruch hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5140d-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
