> [!div class="op_single_selector"]
> * [<span data-ttu-id="b843d-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="b843d-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="b843d-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="b843d-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="b843d-103">C#</span><span class="sxs-lookup"><span data-stu-id="b843d-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="b843d-104">Java</span><span class="sxs-lookup"><span data-stu-id="b843d-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="b843d-105">Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki).</span><span class="sxs-lookup"><span data-stu-id="b843d-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="b843d-106">Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które łączy tooit.</span><span class="sxs-lookup"><span data-stu-id="b843d-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="b843d-107">Użyj twins urządzenia do:</span><span class="sxs-lookup"><span data-stu-id="b843d-107">Use device twins to:</span></span>

* <span data-ttu-id="b843d-108">Przechowywania metadanych urządzenie z Twojego zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b843d-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="b843d-109">Raport bieżące informacje o stanie, takie jak dostępne możliwości i warunki (na przykład hello łączności metodę) z aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b843d-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="b843d-110">Synchronizuj stan hello długotrwałe przepływów pracy (takich jak aktualizacje oprogramowania układowego i konfiguracji), między aplikacją urządzenia i aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b843d-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="b843d-111">Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.</span><span class="sxs-lookup"><span data-stu-id="b843d-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="b843d-112">Twins urządzenia są przeznaczone do synchronizacji i do wykonywania zapytań w konfiguracji urządzeń i warunki.</span><span class="sxs-lookup"><span data-stu-id="b843d-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="b843d-113">Więcej informacje na kiedy toouse twins urządzenie znajduje się w [zrozumieć urządzenia twins][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="b843d-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="b843d-114">Twins urządzeń są przechowywane w Centrum IoT i zawierają:</span><span class="sxs-lookup"><span data-stu-id="b843d-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="b843d-115">*tagi*, dostępny tylko dla hello rozwiązania zaplecza; metadane urządzenia</span><span class="sxs-lookup"><span data-stu-id="b843d-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="b843d-116">*żądany właściwości*, można modyfikować przez rozwiązanie hello obiektów JSON wstecz zakończenia i według przez aplikację urządzenia hello; i</span><span class="sxs-lookup"><span data-stu-id="b843d-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="b843d-117">*zgłoszone właściwości*, można modyfikować przez aplikację urządzenia hello i czytelna dla zaplecza rozwiązania hello obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="b843d-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="b843d-118">Znaczniki i właściwości nie mogą zawierać tablic, ale może być zagnieżdżone obiekty.</span><span class="sxs-lookup"><span data-stu-id="b843d-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="b843d-119">Ponadto zaplecza rozwiązania hello mogą wysyłać zapytania oparte na wszystkich hello powyżej danych twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b843d-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="b843d-120">Odwołuje się zbyt[zrozumieć twins urządzenia] [ lnk-twins] uzyskać więcej informacji o urządzeniu twins i toohello [język zapytań Centrum IoT] [ lnk-query] odwołania na potrzeby zapytań.</span><span class="sxs-lookup"><span data-stu-id="b843d-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="b843d-121">W tej chwili twins urządzenia są dostępne tylko z urządzeń łączących tooIoT Centrum przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="b843d-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="b843d-122">Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="b843d-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="b843d-123">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b843d-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b843d-124">Tworzenie aplikacji zaplecza, który dodaje *tagi* tooa dwie urządzeń i aplikacji symulowane urządzenie, która raportuje łączność kanału jako *podać właściwość* na powitania dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b843d-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="b843d-125">Wyślij zapytanie do urządzeń z zaplecza aplikacji hello tagów i właściwości wcześniej utworzony za pomocą filtrów.</span><span class="sxs-lookup"><span data-stu-id="b843d-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md