> [!div class="op_single_selector"]
> * [<span data-ttu-id="d03f3-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="d03f3-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="d03f3-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="d03f3-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="d03f3-103">C#</span><span class="sxs-lookup"><span data-stu-id="d03f3-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="d03f3-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d03f3-104">Introduction</span></span>

<span data-ttu-id="d03f3-105">W [Rozpoczynanie pracy z Centrum IoT urządzenia twins][lnk-twin-tutorial], wiesz, jak metadanych urządzenia tooset z powrotem rozwiązania kończyć się przy użyciu *tagi*, raport warunków urządzenia z aplikacjami urządzenia przy użyciu *zgłosił właściwości*oraz badanie tych informacji przy użyciu języka przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="d03f3-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="d03f3-106">Z tego samouczka, dowiesz się, jak toouse Witaj dwie urządzenia hello *żądanego właściwości* wraz z *zgłosił właściwości*, tooremotely Konfigurowanie aplikacji dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d03f3-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="d03f3-107">W szczególności w tym samouczku przedstawiono sposób zgłaszania dwie urządzenia oraz odpowiednie właściwości Włącz konfigurację wieloetapowych aplikację dla urządzeń i hello widoczność toohello zaplecza rozwiązania stanu hello tej operacji dla wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d03f3-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="d03f3-108">Można znaleźć więcej informacji na temat roli hello konfiguracji urządzeń w [omówienie zarządzania urządzeniami z Centrum IoT][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="d03f3-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="d03f3-109">Na wysokim poziomie za pomocą urządzenia twins umożliwia hello rozwiązania zaplecza toospecify hello odpowiednią konfigurację hello zarządzanych urządzeń, zamiast wysyłać określonych poleceń.</span><span class="sxs-lookup"><span data-stu-id="d03f3-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="d03f3-110">To powoduje przełączenie urządzenia hello odpowiedzialnym za konfigurowanie hello najlepsze sposób tooupdate jego konfiguracji (bardzo ważne w scenariuszach IoT, których warunki określonego urządzenia wpływać na powitania możliwości tooimmediately wykonania określonych poleceń), podczas raportowania stale toohello zaplecze rozwiązania hello bieżący stan i potencjalne błędy hello procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d03f3-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="d03f3-111">Ten wzorzec jest toohello instrumentalnego zarządzanie dużymi zbiorami urządzeń, jak umożliwia hello rozwiązania zaplecza toohave pełny wgląd stanu hello hello procesu konfiguracji na wszystkich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="d03f3-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="d03f3-112">W scenariuszach, w którym urządzenia są kontrolowane w sposób większej liczby interaktywnych (Włącz wentylator z aplikacji kontrolowane przez użytkownika), należy rozważyć użycie [bezpośrednie metody][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="d03f3-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="d03f3-113">W tym samouczku zmiany zaplecza rozwiązania hello hello telemetrii konfiguracji urządzenia docelowego i, w wyniku którego hello aplikacji urządzenia następuje tooapply wieloetapowych procesu konfiguracji aktualizacji (na przykład oprogramowania modułu ponownego uruchomienia komputera, który to wymaganie Samouczek symuluje z opóźnieniem prosty).</span><span class="sxs-lookup"><span data-stu-id="d03f3-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="d03f3-114">zaplecza rozwiązania Hello przechowywana jest Konfiguracja hello hello urządzenia dwie właściwości żądaną w hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d03f3-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="d03f3-115">Ponieważ konfiguracje mogą zostać obiektu złożonego, zazwyczaj są przypisane unikatowe identyfikatory (skróty lub [identyfikatorów GUID][lnk-guid]) toosimplify ich porównania.</span><span class="sxs-lookup"><span data-stu-id="d03f3-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="d03f3-116">Witaj aplikacji urządzenia raporty bieżącej konfiguracji dublowania hello wymaganą właściwość **telemetryConfig** w hello zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="d03f3-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="d03f3-117">Należy zwrócić uwagę na sposób zgłaszania hello **telemetryConfig** ma dodatkowe właściwości **stanu**, używane tooreport hello stanu procesu aktualizacji konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="d03f3-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="d03f3-118">Po odebraniu nowego wymaganą konfiguracją aplikacji urządzenia hello raportów oczekujących konfiguracji zmieniając hello informacji:</span><span class="sxs-lookup"><span data-stu-id="d03f3-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="d03f3-119">Następnie w późniejszym czasie, hello urządzenia aplikacji będzie zgłaszać hello powodzenie lub niepowodzenie tej operacji, aktualizując hello powyżej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d03f3-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="d03f3-120">Należy zwrócić uwagę, jak zaplecza rozwiązania hello jest w stanie, w dowolnym momencie, stan hello tooquery hello proces konfiguracji wszystkich urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="d03f3-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="d03f3-121">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d03f3-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d03f3-122">Tworzenie aplikacji symulowane urządzenie, który odbiera aktualizacje konfiguracji z zaplecza rozwiązania hello, a następnie raportuje wiele aktualizacji jako *zgłosił właściwości* konfiguracji hello zaktualizować procesu.</span><span class="sxs-lookup"><span data-stu-id="d03f3-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="d03f3-123">Tworzenie zaplecza aplikacji czy aktualizacje hello wymaganą konfiguracją urządzenia, a następnie zapytania hello proces aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d03f3-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
