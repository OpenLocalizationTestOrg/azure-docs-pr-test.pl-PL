## <a name="typical-output"></a><span data-ttu-id="96f5d-101">Najczęściej pojawiające się dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="96f5d-101">Typical output</span></span>

<span data-ttu-id="96f5d-102">Witaj poniższy przykład przedstawia dane wyjściowe hello zapisany plik dziennika toohello przez Przykładowa aplikacja hello Hello World.</span><span class="sxs-lookup"><span data-stu-id="96f5d-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="96f5d-103">dane wyjściowe Hello jest sformatowany dla czytelności:</span><span class="sxs-lookup"><span data-stu-id="96f5d-103">hello output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="96f5d-104">Fragmenty kodu</span><span class="sxs-lookup"><span data-stu-id="96f5d-104">Code snippets</span></span>

<span data-ttu-id="96f5d-105">W tej sekcji omówiono niektóre kluczowe fragmentów kodu hello w hello hello\_próbki world.</span><span class="sxs-lookup"><span data-stu-id="96f5d-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="96f5d-106">Tworzenie bramy krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="96f5d-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="96f5d-107">Musisz zaimplementować *procesu bramy*.</span><span class="sxs-lookup"><span data-stu-id="96f5d-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="96f5d-108">Ten program tworzy hello wewnętrznej infrastruktury (hello broker), ładuje hello krawędzi IoT moduły i konfiguruje hello bramy procesu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="96f5d-109">Krawędź IoT zapewnia hello **bramy\_Utwórz\_z\_JSON** funkcji tooenable toobootstrap bramy z pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="96f5d-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="96f5d-110">Witaj toouse **bramy\_Utwórz\_z\_JSON** działać i przekazać je hello ścieżki tooa JSON pliku, który określa hello tooload modułów IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="96f5d-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="96f5d-111">Kod hello można znaleźć procesu bramy hello w hello *Hello World* przykładowa w hello [main.c] [ lnk-main-c] pliku.</span><span class="sxs-lookup"><span data-stu-id="96f5d-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="96f5d-112">Dla czytelności hello poniższy fragment kodu przedstawia skróconej wersji kod procesu hello bramy.</span><span class="sxs-lookup"><span data-stu-id="96f5d-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="96f5d-113">Ten przykładowy program tworzy bramy, a następnie oczekiwanie hello użytkownika toopress hello **ENTER** klucza przed rys, dół hello bramy.</span><span class="sxs-lookup"><span data-stu-id="96f5d-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="96f5d-114">Plik ustawień JSON Hello zawiera listę tooload modułów krawędzi IoT i hello łącza między modułami hello.</span><span class="sxs-lookup"><span data-stu-id="96f5d-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="96f5d-115">Każdy moduł krawędzi IoT musi określać a:</span><span class="sxs-lookup"><span data-stu-id="96f5d-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="96f5d-116">**Nazwa**: unikatową nazwę dla modułu hello.</span><span class="sxs-lookup"><span data-stu-id="96f5d-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="96f5d-117">**Moduł ładujący**: moduł ładujący, że zna jak tooload hello potrzeby modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="96f5d-118">Moduły ładujące to punkt rozszerzenia służący do ładowania różnych typów modułów.</span><span class="sxs-lookup"><span data-stu-id="96f5d-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="96f5d-119">Krawędź IoT udostępnia ładowarki do użycia z modułami napisane w macierzystym C, Node.js, Java i .NET.</span><span class="sxs-lookup"><span data-stu-id="96f5d-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="96f5d-120">Przykładowa aplikacja Hello Hello World tylko wykorzystuje modułu ładującego hello natywnych C, ponieważ wszystkie moduły hello w tym przykładzie są dynamiczne bibliotek napisana C. Aby uzyskać więcej informacji o tym, jak moduły krawędzi IoT toouse napisane w różnych językach, zobacz hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), lub [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) próbek.</span><span class="sxs-lookup"><span data-stu-id="96f5d-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="96f5d-121">**Nazwa**: hello Nazwa modułu ładującego hello używana tooload hello modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="96f5d-122">**punkt wejścia**: hello ścieżki toohello biblioteką hello modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="96f5d-123">W systemie Linux jest to plik SO, a w systemie Windows — plik DLL.</span><span class="sxs-lookup"><span data-stu-id="96f5d-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="96f5d-124">punkt wejścia Hello jest toohello określonego typu modułu ładującego używane.</span><span class="sxs-lookup"><span data-stu-id="96f5d-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="96f5d-125">punkt wejścia modułu ładującego Node.js Hello jest plikiem js.</span><span class="sxs-lookup"><span data-stu-id="96f5d-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="96f5d-126">punkt wejścia modułu ładującego Java Hello jest ścieżkę i nazwę klasy.</span><span class="sxs-lookup"><span data-stu-id="96f5d-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="96f5d-127">Witaj punktu wejścia modułu ładującego .NET jest nazwa zestawu i nazwa klasy.</span><span class="sxs-lookup"><span data-stu-id="96f5d-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="96f5d-128">**argumenty**: wymaga każdy moduł hello informacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="96f5d-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="96f5d-129">Hello następującego kodu pokazuje hello JSON używane toodeclare wszystkie hello krawędzi IoT modułów Przykładowa aplikacja hello Hello World w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="96f5d-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="96f5d-130">Czy moduł wymaga argumentów, zależy od projektowania hello hello modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="96f5d-131">W tym przykładzie hello rejestratora moduł przyjmuje argument, który jest plik wyjściowy toohello ścieżka hello i hello hello\_world moduł nie ma argumentów.</span><span class="sxs-lookup"><span data-stu-id="96f5d-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="96f5d-132">Plik JSON Hello zawiera również linki hello między modułami hello, które są przekazywane toohello brokera.</span><span class="sxs-lookup"><span data-stu-id="96f5d-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="96f5d-133">Link ma dwie właściwości:</span><span class="sxs-lookup"><span data-stu-id="96f5d-133">A link has two properties:</span></span>

* <span data-ttu-id="96f5d-134">**źródło**: Nazwa modułu, z hello `modules` sekcji lub `\*`.</span><span class="sxs-lookup"><span data-stu-id="96f5d-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="96f5d-135">**obiekt sink**: Nazwa modułu, z hello `modules` sekcji.</span><span class="sxs-lookup"><span data-stu-id="96f5d-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="96f5d-136">Każdy link definiuje trasę i kierunek komunikatów.</span><span class="sxs-lookup"><span data-stu-id="96f5d-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="96f5d-137">Wiadomości powitania **źródła** modułu są dostępne w ramach toohello **zbiornika** modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="96f5d-138">Można ustawić hello **źródła** modułu zbyt`\*`, co oznacza, że hello **zbiornika** modułu odbiera komunikaty z dowolnego modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="96f5d-139">Witaj poniższy kod przedstawia hello JSON używane tooconfigure łącza między modułami hello używane w hello hello\_próbki world w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="96f5d-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="96f5d-140">Każdy komunikat utworzonego przez hello `hello_world` moduł jest używany przez hello `logger` modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="96f5d-141">Publikowanie komunikatów w module hello\_world</span><span class="sxs-lookup"><span data-stu-id="96f5d-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="96f5d-142">Możesz znaleźć kod hello używany przez hello hello\_wiadomości toopublish modułu world hello ["hello_world.c"] [ lnk-helloworld-c] pliku.</span><span class="sxs-lookup"><span data-stu-id="96f5d-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="96f5d-143">Witaj poniższy fragment kodu przedstawia zmieniona wersja kodu hello z komentarze dodane i obsługi usunięte czytelność kodu niektórych błędów:</span><span class="sxs-lookup"><span data-stu-id="96f5d-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="96f5d-144">Przetwarzanie komunikatów w module hello\_world</span><span class="sxs-lookup"><span data-stu-id="96f5d-144">Hello\_world module message processing</span></span>

<span data-ttu-id="96f5d-145">Witaj Witaj\_moduł world nigdy nie przetwarza wiadomości, że inne moduły krawędzi IoT opublikować toohello brokera.</span><span class="sxs-lookup"><span data-stu-id="96f5d-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="96f5d-146">W związku z tym hello wdrożenia wywołania zwrotnego wiadomość hello w Witaj Witaj\_moduł world jest funkcją zerowa.</span><span class="sxs-lookup"><span data-stu-id="96f5d-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="96f5d-147">Publikowanie i przetwarzanie komunikatu przez moduł rejestratora</span><span class="sxs-lookup"><span data-stu-id="96f5d-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="96f5d-148">Moduł rejestratora Hello odbiera komunikaty z brokera hello i zapisuje je w pliku tooa.</span><span class="sxs-lookup"><span data-stu-id="96f5d-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="96f5d-149">Nigdy nie publikuje żadnych komunikatów.</span><span class="sxs-lookup"><span data-stu-id="96f5d-149">It never publishes any messages.</span></span> <span data-ttu-id="96f5d-150">W związku z tym hello kodu modułu rejestratora hello nigdy nie wywołuje hello **Broker_Publish** funkcji.</span><span class="sxs-lookup"><span data-stu-id="96f5d-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="96f5d-151">Witaj **Logger_Receive** funkcji w hello [logger.c] [ lnk-logger-c] plik jest hello wywołania zwrotnego hello brokera wywołuje toodeliver wiadomości toohello rejestratora modułu.</span><span class="sxs-lookup"><span data-stu-id="96f5d-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="96f5d-152">Witaj poniższy fragment kodu przedstawia zmienionej wersji z komentarze dodane i obsługi usunięte czytelność kodu niektórych błędów:</span><span class="sxs-lookup"><span data-stu-id="96f5d-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="96f5d-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96f5d-153">Next steps</span></span>

<span data-ttu-id="96f5d-154">W tym artykule został uruchomiony proste brama brzegowa IoT, który zapisuje plik dziennika tooa wiadomości.</span><span class="sxs-lookup"><span data-stu-id="96f5d-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="96f5d-155">toorun przykład, który wysyła wiadomości tooIoT Centrum, zobacz [krawędzi IoT — wysyłanie wiadomości urządzenia do chmury z symulowane urządzenie przy użyciu systemu Linux] [ lnk-gateway-simulated-linux] lub [krawędzi IoT — wysyłać z urządzenia do chmury Symulowane urządzenie przy użyciu systemu Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="96f5d-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md