## <a name="overview"></a><span data-ttu-id="f98ac-101">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f98ac-101">Overview</span></span>

<span data-ttu-id="f98ac-102">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f98ac-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="f98ac-103">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f98ac-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="f98ac-104">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f98ac-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="f98ac-105">Konfigurowanie toocommunicate Twojego urządzenia do komputera i hello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f98ac-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="f98ac-106">Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać symulowanych dane telemetryczne można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="f98ac-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f98ac-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f98ac-107">Prerequisites</span></span>

<span data-ttu-id="f98ac-108">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f98ac-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f98ac-109">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f98ac-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f98ac-110">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="f98ac-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="f98ac-111">Wymagane oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="f98ac-111">Required software</span></span>

<span data-ttu-id="f98ac-112">Należy klient SSH na Twojej tooenable komputerów możesz tooremotely dostępu hello wiersza polecenia na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f98ac-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="f98ac-113">System Windows nie zawiera klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="f98ac-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="f98ac-114">Firma Microsoft zaleca używanie [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="f98ac-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="f98ac-115">Większość dystrybucje systemu Linux i Mac OS obejmują narzędzia wiersza polecenia SSH hello.</span><span class="sxs-lookup"><span data-stu-id="f98ac-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="f98ac-116">Aby uzyskać więcej informacji, zobacz [SSH za pomocą systemu Linux lub Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="f98ac-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="f98ac-117">Wymagany sprzęt</span><span class="sxs-lookup"><span data-stu-id="f98ac-117">Required hardware</span></span>

<span data-ttu-id="f98ac-118">Tooenable komputer stacjonarny tooconnect można zdalnie toohello wiersza polecenia na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f98ac-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="f98ac-119">[Microsoft IoT Starter Kit malina Pi 3] [ lnk-starter-kits] lub równoważne składników.</span><span class="sxs-lookup"><span data-stu-id="f98ac-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="f98ac-120">W tym samouczku korzysta z poniższych elementów z zestawu hello hello:</span><span class="sxs-lookup"><span data-stu-id="f98ac-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="f98ac-121">Pi malinowe 3</span><span class="sxs-lookup"><span data-stu-id="f98ac-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="f98ac-122">Karta MicroSD (z NOOBS)</span><span class="sxs-lookup"><span data-stu-id="f98ac-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="f98ac-123">Kabla USB Mini</span><span class="sxs-lookup"><span data-stu-id="f98ac-123">A USB Mini cable</span></span>
- <span data-ttu-id="f98ac-124">Kabla Ethernet</span><span class="sxs-lookup"><span data-stu-id="f98ac-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/