> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ff1e-101">Linux</span><span class="sxs-lookup"><span data-stu-id="7ff1e-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="7ff1e-102">Windows</span><span class="sxs-lookup"><span data-stu-id="7ff1e-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="7ff1e-103">Ten artykuł zawiera szczegółowe wskazówki dotyczące hello [Hello World przykładowy kod] [ lnk-helloworld-sample] tooillustrate hello podstawowych składników hello [Azure IoT krawędzi] [ lnk-iot-edge] architektury.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="7ff1e-104">Witaj w przykładzie użyto hello Azure IoT krawędzi toobuild proste bramy, która rejestruje co pięć sekund pliku tooa komunikat "hello world".</span><span class="sxs-lookup"><span data-stu-id="7ff1e-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="7ff1e-105">Przewodnik składa się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="7ff1e-105">This walkthrough covers:</span></span>

* <span data-ttu-id="7ff1e-106">**Hello World przykładowa architektura**: w tym artykule opisano sposób [pojęcia architektury Azure IoT krawędzi] [ lnk-edge-concepts] się przykład Witaj świecie toohello oraz sposób składniki hello dopasowania.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="7ff1e-107">**Jak toobuild hello próbki**: hello kroki wymagane toobuild hello próbki.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="7ff1e-108">**Jak toorun hello próbki**: hello kroki wymagane toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="7ff1e-109">**Dane wyjściowe zazwyczaj**: przykład hello output tooexpect po uruchomieniu hello próbki.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="7ff1e-110">**Wstawki kodu**: kolekcja tooshow wstawki kodu jak przykładowa aplikacja hello Hello World implementuje klucza składniki bramy IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="7ff1e-111">Przykładowa architektura Witaj, świecie</span><span class="sxs-lookup"><span data-stu-id="7ff1e-111">Hello World sample architecture</span></span>
<span data-ttu-id="7ff1e-112">Przykładowa aplikacja Hello Hello World przedstawiono hello pojęcia opisane w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="7ff1e-113">Przykładowa aplikacja Hello Hello World implementuje bramy IoT krawędzi, która ma potoku składają się z dwóch modułów krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="7ff1e-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="7ff1e-114">Witaj *Witaj świecie* moduł tworzy komunikat co pięć sekund i przekazuje je toohello rejestratora modułu.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="7ff1e-115">Witaj *rejestratora* wiadomości powitania zapisy modułu odbierze tooa pliku.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Architektura przykładowej aplikacji Hello world utworzonej przy użyciu usługi Azure IoT Edge][4]

<span data-ttu-id="7ff1e-117">Zgodnie z opisem w poprzedniej sekcji hello, hello World Hello modułu nie zostały spełnione komunikatów bezpośrednio modułu rejestratora toohello co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="7ff1e-118">Zamiast tego należy go publikuje brokera toohello komunikatów co pięć sekund.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="7ff1e-119">Moduł rejestratora Hello odbiera wiadomości powitania od brokera hello i działa na niego, zapisywanie hello zawartość pliku tooa wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="7ff1e-120">Moduł rejestratora Hello wykorzystuje tylko komunikaty z hello brokera, nigdy nie publikuje nowy brokera toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Jak brokera hello tras wiadomości między modułami w programie Azure IoT Edge][5]

<span data-ttu-id="7ff1e-122">Witaj ilustracji powyżej przedstawiono architekturę hello Przykładowa aplikacja hello Hello World i ścieżek względnych hello toohello pliki źródłowe, które implementuje różnych części próbki hello w hello [repozytorium][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="7ff1e-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="7ff1e-123">Eksploruj hello kod na własną lub hello wstawki kodu za pomocą poniżej jako przewodnika.</span><span class="sxs-lookup"><span data-stu-id="7ff1e-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md