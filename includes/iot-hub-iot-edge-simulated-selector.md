> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa210-101">Linux</span><span class="sxs-lookup"><span data-stu-id="aa210-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="aa210-102">Windows</span><span class="sxs-lookup"><span data-stu-id="aa210-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="aa210-103">Ten przewodnik [symulowane urządzenie chmury Przekaż przykładowe] przedstawiono sposób użycia [Azure IoT krawędzi] [ lnk-sdk] do wysyłania danych telemetrycznych urządzenia do chmury do Centrum IoT z symulowanego urządzenia .</span><span class="sxs-lookup"><span data-stu-id="aa210-103">This walkthrough of the [Simulated Device Cloud Upload sample] shows you how to use [Azure IoT Edge][lnk-sdk] to send device-to-cloud telemetry to IoT Hub from simulated devices.</span></span>

<span data-ttu-id="aa210-104">Przewodnik składa się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="aa210-104">This walkthrough covers:</span></span>

* <span data-ttu-id="aa210-105">**Architektura**: architektury informacji na temat [symulowane urządzenie chmury Przekaż przykładowe].</span><span class="sxs-lookup"><span data-stu-id="aa210-105">**Architecture**: architectural information about the [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="aa210-106">**Kompilowanie i uruchamianie**: czynności wymagane do skompilowania i uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="aa210-106">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="aa210-107">Architektura</span><span class="sxs-lookup"><span data-stu-id="aa210-107">Architecture</span></span>

<span data-ttu-id="aa210-108">[symulowane urządzenie chmury Przekaż przykładowe] przedstawiono sposób tworzenia bramy, która wysyła dane telemetryczne z symulowanego urządzenia do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-108">The [Simulated Device Cloud Upload sample] shows how to create a gateway that sends telemetry from simulated devices to an IoT hub.</span></span> <span data-ttu-id="aa210-109">Urządzenie może nie móc połączyć się bezpośrednio z Centrum IoT, ponieważ urządzenie:</span><span class="sxs-lookup"><span data-stu-id="aa210-109">A device may not be able to connect directly to IoT Hub because the device:</span></span>

* <span data-ttu-id="aa210-110">Nie używa protokołu komunikacji rozpoznawany przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="aa210-111">Nie jest inteligentne do zapamiętania tożsamość przypisana przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-111">Is not smart enough to remember the identity assigned to it by IoT Hub.</span></span>

<span data-ttu-id="aa210-112">Brama brzegowa IoT umożliwia rozwiązanie tych problemów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="aa210-112">An IoT Edge gateway can solve these problems in the following ways:</span></span>

* <span data-ttu-id="aa210-113">Brama rozumie protokół używany przez urządzenie odbiera telemetrię urządzenia do chmury z urządzenia i przesyła dalej wiadomości do Centrum IoT przy użyciu protokołu rozpoznawany przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-113">The gateway understands the protocol used by the device, receives device-to-cloud telemetry from the device, and forwards those messages to IoT Hub using a protocol understood by the IoT hub.</span></span>

* <span data-ttu-id="aa210-114">Brama mapuje tożsamości Centrum IoT na urządzeniach i działa jako serwer proxy, gdy urządzenie wysyła komunikaty do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-114">The gateway maps IoT Hub identities to devices and acts as a proxy when a device sends messages to IoT Hub.</span></span>

<span data-ttu-id="aa210-115">Na poniższym diagramie przedstawiono główne składniki próbki, łącznie z modułów krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="aa210-115">The following diagram shows the main components of the sample, including the IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="aa210-116">Moduły nie przekazują komunikatów bezpośrednio między sobą.</span><span class="sxs-lookup"><span data-stu-id="aa210-116">The modules do not pass messages directly to each other.</span></span> <span data-ttu-id="aa210-117">Moduły publikowania komunikatów wewnętrzny brokera, która dostarcza wiadomości do innych modułów przy użyciu mechanizmu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="aa210-117">The modules publish messages to an internal broker that delivers the messages to the other modules using a subscription mechanism.</span></span> <span data-ttu-id="aa210-118">Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure IoT krawędzi][lnk-gw-getstarted].</span><span class="sxs-lookup"><span data-stu-id="aa210-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="aa210-119">Moduł pozyskiwania protokołu</span><span class="sxs-lookup"><span data-stu-id="aa210-119">Protocol ingestion module</span></span>

<span data-ttu-id="aa210-120">Ten moduł jest punkt początkowy odbierania danych z urządzeń, za pośrednictwem bramy i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="aa210-120">This module is the starting point for receiving data from devices, through the gateway, and into the cloud.</span></span> <span data-ttu-id="aa210-121">W przykładowym modułu:</span><span class="sxs-lookup"><span data-stu-id="aa210-121">In the sample, the module:</span></span>

1. <span data-ttu-id="aa210-122">Tworzy symulowane temperatury danych.</span><span class="sxs-lookup"><span data-stu-id="aa210-122">Creates simulated temperature data.</span></span> <span data-ttu-id="aa210-123">Jeśli używasz urządzenia fizyczne moduł odczytuje dane z tych urządzeń fizycznych.</span><span class="sxs-lookup"><span data-stu-id="aa210-123">If you use physical devices, the module reads data from those physical devices.</span></span>
1. <span data-ttu-id="aa210-124">Tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="aa210-124">Creates a message.</span></span>
1. <span data-ttu-id="aa210-125">Umieszczenie danych symulowane temperatury w treści wiadomości.</span><span class="sxs-lookup"><span data-stu-id="aa210-125">Places the simulated temperature data into the message content.</span></span>
1. <span data-ttu-id="aa210-126">Dodaje właściwość fałszywy adres MAC do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="aa210-126">Adds a property with a fake MAC address to the message.</span></span>
1. <span data-ttu-id="aa210-127">Udostępnia komunikat do następnego modułu w łańcuchu.</span><span class="sxs-lookup"><span data-stu-id="aa210-127">Makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="aa210-128">Moduł o nazwie **wprowadzanie protokołu X** poprzedni diagram nosi nazwę **symulowane urządzenie** w kodzie źródłowym.</span><span class="sxs-lookup"><span data-stu-id="aa210-128">The module called **Protocol X ingestion** in the previous diagram is called **Simulated device** in the source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="aa210-129">Adres MAC &lt;-&gt; moduł identyfikatora usługi IoT Hub</span><span class="sxs-lookup"><span data-stu-id="aa210-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="aa210-130">Ten moduł skanowania pod kątem wiadomości, których właściwość adres Mac.</span><span class="sxs-lookup"><span data-stu-id="aa210-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="aa210-131">W przykładzie moduł wprowadzanie protokołu dodaje właściwość adres MAC.</span><span class="sxs-lookup"><span data-stu-id="aa210-131">In the sample, the protocol ingestion module adds the MAC address property.</span></span> <span data-ttu-id="aa210-132">Jeśli moduł znajdzie takich właściwości, dodaje innej właściwości przy użyciu klucza urządzenia IoT Hub do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="aa210-132">If the module finds such a property, it adds another property with an IoT Hub device key to the message.</span></span> <span data-ttu-id="aa210-133">Moduł następnie udostępnia komunikat do następnego modułu w łańcuchu.</span><span class="sxs-lookup"><span data-stu-id="aa210-133">The module then makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="aa210-134">Deweloper konfiguruje mapowanie między tożsamości Centrum IoT i adresów MAC do skojarzenia symulowanego urządzenia z Centrum IoT tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="aa210-134">The developer sets up a mapping between MAC addresses and IoT Hub identities to associate the simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="aa210-135">Deweloper ręcznie dodaje mapowania w ramach konfiguracji modułu.</span><span class="sxs-lookup"><span data-stu-id="aa210-135">The developer adds the mapping manually as part of the module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="aa210-136">W tym przykładzie adres MAC jest używany jako unikatowy identyfikator urządzenia i jest korelowany z tożsamością urządzenia usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aa210-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="aa210-137">Możesz jednak napisać swój własny moduł, który będzie używał innego unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="aa210-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="aa210-138">Na przykład urządzenia może mieć unikatowe numery seryjne lub dane telemetryczne mogą obejmować nazwę unikatową urządzenia osadzonego.</span><span class="sxs-lookup"><span data-stu-id="aa210-138">For example, your devices may have unique serial numbers or the telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="aa210-139">Moduł komunikacyjny usługi IoT Hub</span><span class="sxs-lookup"><span data-stu-id="aa210-139">IoT Hub communication module</span></span>

<span data-ttu-id="aa210-140">Ten moduł ma komunikatów z Centrum IoT urządzenia właściwości klucza, która została przypisana w poprzednim module.</span><span class="sxs-lookup"><span data-stu-id="aa210-140">This module takes messages with an IoT Hub device key property that was assigned by the previous module.</span></span> <span data-ttu-id="aa210-141">Moduł wysyła zawartość komunikatu do Centrum IoT przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="aa210-141">The module sends the message content to IoT Hub using the HTTP protocol.</span></span> <span data-ttu-id="aa210-142">Protokółu HTTP jest jednym z trzech protokołów obsługiwanych przez usługę IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aa210-142">HTTP is one of the three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="aa210-143">Zamiast otwarcie połączenia dla każdego symulowanego urządzenia, ten moduł otwiera pojedynczego połączenia HTTP z bramy z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="aa210-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from the gateway to the IoT hub.</span></span> <span data-ttu-id="aa210-144">Moduł następnie multiplexes połączenia z symulowanego urządzenia za pośrednictwem tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="aa210-144">The module then multiplexes connections from all the simulated devices over that connection.</span></span> <span data-ttu-id="aa210-145">Takie podejście umożliwia pojedyncza brama do łączenia wielu więcej urządzeń.</span><span class="sxs-lookup"><span data-stu-id="aa210-145">This approach enables a single gateway to connect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="aa210-146">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="aa210-146">Before you get started</span></span>

<span data-ttu-id="aa210-147">Przed rozpoczęciem pracy należy:</span><span class="sxs-lookup"><span data-stu-id="aa210-147">Before you get started, you must:</span></span>

* <span data-ttu-id="aa210-148">[Tworzenie Centrum IoT] [ lnk-create-hub] w Twojej subskrypcji platformy Azure, potrzebna jest nazwa Centrum w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="aa210-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="aa210-149">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="aa210-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="aa210-150">Dodaj dwa urządzenia do Centrum IoT i zanotuj ich identyfikatorów i klucze urządzenia.</span><span class="sxs-lookup"><span data-stu-id="aa210-150">Add two devices to your IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="aa210-151">Można użyć [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia do dodania urządzenia do Centrum IoT utworzony w poprzednim kroku i pobieranie ich kluczy.</span><span class="sxs-lookup"><span data-stu-id="aa210-151">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span></span>

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
<span data-ttu-id="aa210-152">[symulowane urządzenie chmury Przekaż przykładowe]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span><span class="sxs-lookup"><span data-stu-id="aa210-152">[Simulated Device Cloud Upload sample]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span></span>
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md