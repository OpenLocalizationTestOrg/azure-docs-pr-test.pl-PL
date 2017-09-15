> [!div class="op_single_selector"]
> * [<span data-ttu-id="61c48-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="61c48-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="61c48-102">C#/node.js</span><span class="sxs-lookup"><span data-stu-id="61c48-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="61c48-103">C#</span><span class="sxs-lookup"><span data-stu-id="61c48-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="61c48-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="61c48-104">Introduction</span></span>

<span data-ttu-id="61c48-105">W [Rozpoczynanie pracy z Centrum IoT urządzenia twins][lnk-twin-tutorial], wiesz, jak ustawić metadane urządzenia z pomocą zaplecza rozwiązania *tagi*, raport warunków urządzenia z aplikacjami urządzenia przy użyciu *zgłosił właściwości*oraz badanie tych informacji przy użyciu języka przypominającego SQL.</span><span class="sxs-lookup"><span data-stu-id="61c48-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how to set device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="61c48-106">Z tego samouczka, dowiesz sposób użycia dwie urządzenia *żądanego właściwości* wraz z *zgłosił właściwości*, w celu zdalnego konfigurowania aplikacji dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="61c48-106">In this tutorial, you will learn how to use the the device twin's *desired properties* along with *reported properties*, to remotely configure device apps.</span></span> <span data-ttu-id="61c48-107">W szczególności w tym samouczku przedstawiono sposób zgłaszania dwie urządzenia oraz odpowiednie właściwości Włącz konfigurację wieloetapowych aplikację dla urządzeń i widoczności do zaplecza rozwiązania stanu tej operacji dla wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="61c48-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide the visibility to the solution back end of the status of this operation across all devices.</span></span> <span data-ttu-id="61c48-108">Można znaleźć więcej informacji na temat roli konfiguracji urządzeń w [omówienie zarządzania urządzeniami z Centrum IoT][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="61c48-108">You can find more information regarding the role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="61c48-109">Na wysokim poziomie za pomocą urządzenia twins umożliwia zaplecza rozwiązania określić odpowiednią konfigurację dla zarządzanych urządzeń, zamiast wysyłać określonych poleceń.</span><span class="sxs-lookup"><span data-stu-id="61c48-109">At a high level, using device twins enables the solution back end to specify the desired configuration for the managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="61c48-110">To powoduje przełączenie urządzenia odpowiedzialnym za konfigurowanie najlepszy sposób, aby zaktualizować konfigurację (bardzo ważne w scenariuszach IoT, których warunki określonego urządzenia wpłynąć negatywnie na natychmiast wykonać określonych poleceń), podczas raportowania stale do rozwiązania Zakończ bieżący stan i potencjalnych błędów procesu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="61c48-110">This puts the device in charge of setting up the best way to update its configuration (very important in IoT scenarios where specific device conditions affect the ability to immediately carry out specific commands), while continually reporting to the solution back end the current state and potential error conditions of the update process.</span></span> <span data-ttu-id="61c48-111">Ten wzorzec jest urządzeń do zarządzania dużych zestawów urządzeń, ponieważ umożliwia ona zaplecza rozwiązania mieć pełny wgląd w stan procesu konfiguracji na wszystkich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="61c48-111">This pattern is instrumental to the management of large sets of devices, as it enables the solution back end to have full visibility of the state of the configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="61c48-112">W scenariuszach, w którym urządzenia są kontrolowane w sposób większej liczby interaktywnych (Włącz wentylator z aplikacji kontrolowane przez użytkownika), należy rozważyć użycie [bezpośrednie metody][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="61c48-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="61c48-113">W tym samouczku zaplecza rozwiązania umożliwia zmianę konfiguracji telemetrii urządzenia docelowego i, w związku z tym, że aplikacji urządzenia jest zgodna z procesu wieloetapowych, aby zastosować aktualizację konfiguracji (na przykład wymaganie oprogramowania modułu ponownego uruchomienia komputera, którym znajduje się ten samouczek symuluje z opóźnieniem prosty).</span><span class="sxs-lookup"><span data-stu-id="61c48-113">In this tutorial, the solution back end changes the telemetry configuration of a target device and, as a result of that, the device app follows a multi-step process to apply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="61c48-114">Zaplecze rozwiązania przechowuje konfigurację w odpowiednich właściwościach dwie urządzenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="61c48-114">The solution back end stores the configuration in the device twin's desired properties in the following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="61c48-115">Ponieważ konfiguracje mogą zostać obiektu złożonego, zazwyczaj są przypisane unikatowe identyfikatory (skróty lub [identyfikatorów GUID][lnk-guid]) aby uprościć ich porównania.</span><span class="sxs-lookup"><span data-stu-id="61c48-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) to simplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="61c48-116">Aplikacji urządzenia raporty bieżącej konfiguracji dublowania żądanej właściwości **telemetryConfig** we właściwościach zgłoszone:</span><span class="sxs-lookup"><span data-stu-id="61c48-116">The device app reports its current configuration mirroring the desired property **telemetryConfig** in the reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="61c48-117">Uwaga jak opisane **telemetryConfig** ma dodatkowe właściwości **stanu**, używana do raportowania stanu procesu aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61c48-117">Note how the reported **telemetryConfig** has an additional property **status**, used to report the state of the configuration update process.</span></span>

<span data-ttu-id="61c48-118">Po odebraniu nowego wymaganą konfiguracją aplikacji urządzenia raportów oczekujących konfiguracji, zmieniając informacje:</span><span class="sxs-lookup"><span data-stu-id="61c48-118">When a new desired configuration is received, the device app reports a pending configuration by changing the information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="61c48-119">Następnie w późniejszym czasie, aplikacji urządzenia zgłosi powodzenie lub niepowodzenie tej operacji przez modyfikowanie właściwości powyżej.</span><span class="sxs-lookup"><span data-stu-id="61c48-119">Then, at some later time, the device app will report the success or failure of this operation by updating the above property.</span></span>
<span data-ttu-id="61c48-120">Należy zwrócić uwagę, jak zaplecza rozwiązania jest w stanie, w dowolnym momencie można zbadać stanu procesu konfiguracji na wszystkich urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="61c48-120">Note how the solution back end is able, at any time, to query the status of the configuration process across all the devices.</span></span>

<span data-ttu-id="61c48-121">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="61c48-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="61c48-122">Tworzenie aplikacji symulowane urządzenie, który odbiera aktualizacje konfiguracji z zaplecza rozwiązania, a następnie raportuje wiele aktualizacji jako *zgłosił właściwości* w konfiguracji zaktualizować procesu.</span><span class="sxs-lookup"><span data-stu-id="61c48-122">Create a simulated device app that receives configuration updates from the solution back end, and reports multiple updates as *reported properties* on the configuration update process.</span></span>
* <span data-ttu-id="61c48-123">Tworzenie aplikacji zaplecza, aktualizuje odpowiednią konfigurację urządzenia, a następnie za pośrednictwem procesu aktualizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="61c48-123">Create a back-end app that updates the desired configuration of a device, and then queries the configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
