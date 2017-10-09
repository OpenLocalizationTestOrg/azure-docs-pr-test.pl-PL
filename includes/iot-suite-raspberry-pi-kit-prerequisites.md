## <a name="prerequisites"></a><span data-ttu-id="be18f-101">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be18f-101">Prerequisites</span></span>

<span data-ttu-id="be18f-102">toocomplete tego samouczka należy aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="be18f-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="be18f-103">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="be18f-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="be18f-104">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="be18f-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="be18f-105">Wymagane oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="be18f-105">Required software</span></span>

<span data-ttu-id="be18f-106">Należy klient SSH na Twojej tooenable komputerów możesz tooremotely dostępu hello wiersza polecenia na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="be18f-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="be18f-107">System Windows nie zawiera klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="be18f-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="be18f-108">Firma Microsoft zaleca używanie [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="be18f-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="be18f-109">Większość dystrybucje systemu Linux i Mac OS obejmują narzędzia wiersza polecenia SSH hello.</span><span class="sxs-lookup"><span data-stu-id="be18f-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="be18f-110">Aby uzyskać więcej informacji, zobacz [SSH za pomocą systemu Linux lub Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span><span class="sxs-lookup"><span data-stu-id="be18f-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="be18f-111">Wymagany sprzęt</span><span class="sxs-lookup"><span data-stu-id="be18f-111">Required hardware</span></span>

<span data-ttu-id="be18f-112">Tooenable komputer stacjonarny tooconnect można zdalnie toohello wiersza polecenia na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="be18f-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="be18f-113">[Microsoft IoT Starter Kit malina Pi 3] [ lnk-starter-kits] lub równoważne składników.</span><span class="sxs-lookup"><span data-stu-id="be18f-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="be18f-114">W tym samouczku korzysta z poniższych elementów z zestawu hello hello:</span><span class="sxs-lookup"><span data-stu-id="be18f-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="be18f-115">Pi malinowe 3</span><span class="sxs-lookup"><span data-stu-id="be18f-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="be18f-116">Karta MicroSD (z NOOBS)</span><span class="sxs-lookup"><span data-stu-id="be18f-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="be18f-117">Kabla USB Mini</span><span class="sxs-lookup"><span data-stu-id="be18f-117">A USB Mini cable</span></span>
- <span data-ttu-id="be18f-118">Kabla Ethernet</span><span class="sxs-lookup"><span data-stu-id="be18f-118">An Ethernet cable</span></span>
- <span data-ttu-id="be18f-119">Czujnik BME280</span><span class="sxs-lookup"><span data-stu-id="be18f-119">BME280 sensor</span></span>
- <span data-ttu-id="be18f-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="be18f-120">Breadboard</span></span>
- <span data-ttu-id="be18f-121">Przewodów zworek</span><span class="sxs-lookup"><span data-stu-id="be18f-121">Jumper wires</span></span>
- <span data-ttu-id="be18f-122">Rezystory</span><span class="sxs-lookup"><span data-stu-id="be18f-122">Resistors</span></span>
- <span data-ttu-id="be18f-123">LED</span><span class="sxs-lookup"><span data-stu-id="be18f-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/