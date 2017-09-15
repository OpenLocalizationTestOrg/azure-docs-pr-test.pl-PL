> [!div class="op_single_selector"]
> * [<span data-ttu-id="6349b-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="6349b-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="6349b-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="6349b-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="6349b-103">C#</span><span class="sxs-lookup"><span data-stu-id="6349b-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="6349b-104">Java</span><span class="sxs-lookup"><span data-stu-id="6349b-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="6349b-105">Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki).</span><span class="sxs-lookup"><span data-stu-id="6349b-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6349b-106">Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które nawiązuje z nim połączenie.</span><span class="sxs-lookup"><span data-stu-id="6349b-106">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="6349b-107">Użyj twins urządzenia do:</span><span class="sxs-lookup"><span data-stu-id="6349b-107">Use device twins to:</span></span>

* <span data-ttu-id="6349b-108">Przechowywania metadanych urządzenie z Twojego zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6349b-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="6349b-109">Raport bieżące informacje o stanie, takie jak dostępne możliwości i warunki (na przykład łączności metodę) z aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6349b-109">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="6349b-110">Synchronizuj stan długotrwałe przepływów pracy (takich jak aktualizacje oprogramowania układowego i konfiguracji), między aplikacją urządzenia i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="6349b-110">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="6349b-111">Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.</span><span class="sxs-lookup"><span data-stu-id="6349b-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="6349b-112">Twins urządzenia są przeznaczone do synchronizacji i do wykonywania zapytań w konfiguracji urządzeń i warunki.</span><span class="sxs-lookup"><span data-stu-id="6349b-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="6349b-113">Więcej informacje o tym, kiedy używać twins urządzenia znajdują się w [zrozumieć urządzenia twins][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="6349b-113">More informations on when to use device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="6349b-114">Twins urządzeń są przechowywane w Centrum IoT i zawierają:</span><span class="sxs-lookup"><span data-stu-id="6349b-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="6349b-115">*tagi*, metadane urządzenia jest dostępne tylko dla zaplecza rozwiązania;</span><span class="sxs-lookup"><span data-stu-id="6349b-115">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="6349b-116">*żądany właściwości*, obiektów JSON można modyfikować przy użyciu rozwiązania wstecz zakończenia i według przez aplikację urządzenia, a</span><span class="sxs-lookup"><span data-stu-id="6349b-116">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="6349b-117">*zgłoszone właściwości*, obiektów JSON można modyfikować za pomocą aplikacji urządzenia i czytelna dla zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6349b-117">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="6349b-118">Znaczniki i właściwości nie mogą zawierać tablic, ale może być zagnieżdżone obiekty.</span><span class="sxs-lookup"><span data-stu-id="6349b-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="6349b-119">Ponadto zaplecza rozwiązania można badać twins urządzenia na podstawie danych powyżej.</span><span class="sxs-lookup"><span data-stu-id="6349b-119">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="6349b-120">Zapoznaj się [zrozumieć twins urządzenia] [ lnk-twins] Aby uzyskać więcej informacji o urządzeniu twins oraz [język zapytań Centrum IoT] [ lnk-query] odwołania dla wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="6349b-120">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="6349b-121">W tej chwili twins urządzenia są dostępne tylko z urządzeń łączących się za pomocą protokołu MQTT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6349b-121">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="6349b-122">Zapoznaj się z [Obsługa MQTT] [ lnk-devguide-mqtt] artykułu instrukcje na temat do konwersji istniejącej aplikacji urządzenia do używania MQTT.</span><span class="sxs-lookup"><span data-stu-id="6349b-122">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>

<span data-ttu-id="6349b-123">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="6349b-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6349b-124">Tworzenie aplikacji zaplecza, który dodaje *tagi* dwie urządzeń i aplikacji symulowane urządzenie, która raportuje kanału łączności jako *podać właściwość* na dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6349b-124">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="6349b-125">Wyślij zapytanie do urządzeń z zaplecza aplikacji przy użyciu filtrów na temat właściwości wcześniej utworzony i tagów.</span><span class="sxs-lookup"><span data-stu-id="6349b-125">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md