## <a name="typical-output"></a>Najczęściej pojawiające się dane wyjściowe

Witaj poniższy przykład przedstawia dane wyjściowe hello zapisany plik dziennika toohello przez Przykładowa aplikacja hello Hello World. dane wyjściowe Hello jest sformatowany dla czytelności:

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

## <a name="code-snippets"></a>Fragmenty kodu

W tej sekcji omówiono niektóre kluczowe fragmentów kodu hello w hello hello\_próbki world.

### <a name="iot-edge-gateway-creation"></a>Tworzenie bramy krawędzi IoT

Musisz zaimplementować *procesu bramy*. Ten program tworzy hello wewnętrznej infrastruktury (hello broker), ładuje hello krawędzi IoT moduły i konfiguruje hello bramy procesu. Krawędź IoT zapewnia hello **bramy\_Utwórz\_z\_JSON** funkcji tooenable toobootstrap bramy z pliku JSON. Witaj toouse **bramy\_Utwórz\_z\_JSON** działać i przekazać je hello ścieżki tooa JSON pliku, który określa hello tooload modułów IoT krawędzi.

Kod hello można znaleźć procesu bramy hello w hello *Hello World* przykładowa w hello [main.c] [ lnk-main-c] pliku. Dla czytelności hello poniższy fragment kodu przedstawia skróconej wersji kod procesu hello bramy. Ten przykładowy program tworzy bramy, a następnie oczekiwanie hello użytkownika toopress hello **ENTER** klucza przed rys, dół hello bramy.

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

Plik ustawień JSON Hello zawiera listę tooload modułów krawędzi IoT i hello łącza między modułami hello. Każdy moduł krawędzi IoT musi określać a:

* **Nazwa**: unikatową nazwę dla modułu hello.
* **Moduł ładujący**: moduł ładujący, że zna jak tooload hello potrzeby modułu. Moduły ładujące to punkt rozszerzenia służący do ładowania różnych typów modułów. Krawędź IoT udostępnia ładowarki do użycia z modułami napisane w macierzystym C, Node.js, Java i .NET. Przykładowa aplikacja Hello Hello World tylko wykorzystuje modułu ładującego hello natywnych C, ponieważ wszystkie moduły hello w tym przykładzie są dynamiczne bibliotek napisana C. Aby uzyskać więcej informacji o tym, jak moduły krawędzi IoT toouse napisane w różnych językach, zobacz hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), lub [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) próbek.
    * **Nazwa**: hello Nazwa modułu ładującego hello używana tooload hello modułu.
    * **punkt wejścia**: hello ścieżki toohello biblioteką hello modułu. W systemie Linux jest to plik SO, a w systemie Windows — plik DLL. punkt wejścia Hello jest toohello określonego typu modułu ładującego używane. punkt wejścia modułu ładującego Node.js Hello jest plikiem js. punkt wejścia modułu ładującego Java Hello jest ścieżkę i nazwę klasy. Witaj punktu wejścia modułu ładującego .NET jest nazwa zestawu i nazwa klasy.

* **argumenty**: wymaga każdy moduł hello informacji konfiguracji.

Hello następującego kodu pokazuje hello JSON używane toodeclare wszystkie hello krawędzi IoT modułów Przykładowa aplikacja hello Hello World w systemie Linux. Czy moduł wymaga argumentów, zależy od projektowania hello hello modułu. W tym przykładzie hello rejestratora moduł przyjmuje argument, który jest plik wyjściowy toohello ścieżka hello i hello hello\_world moduł nie ma argumentów.

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

Plik JSON Hello zawiera również linki hello między modułami hello, które są przekazywane toohello brokera. Link ma dwie właściwości:

* **źródło**: Nazwa modułu, z hello `modules` sekcji lub `\*`.
* **obiekt sink**: Nazwa modułu, z hello `modules` sekcji.

Każdy link definiuje trasę i kierunek komunikatów. Wiadomości powitania **źródła** modułu są dostępne w ramach toohello **zbiornika** modułu. Można ustawić hello **źródła** modułu zbyt`\*`, co oznacza, że hello **zbiornika** modułu odbiera komunikaty z dowolnego modułu.

Witaj poniższy kod przedstawia hello JSON używane tooconfigure łącza między modułami hello używane w hello hello\_próbki world w systemie Linux. Każdy komunikat utworzonego przez hello `hello_world` moduł jest używany przez hello `logger` modułu.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Publikowanie komunikatów w module hello\_world

Możesz znaleźć kod hello używany przez hello hello\_wiadomości toopublish modułu world hello ["hello_world.c"] [ lnk-helloworld-c] pliku. Witaj poniższy fragment kodu przedstawia zmieniona wersja kodu hello z komentarze dodane i obsługi usunięte czytelność kodu niektórych błędów:

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

### <a name="helloworld-module-message-processing"></a>Przetwarzanie komunikatów w module hello\_world

Witaj Witaj\_moduł world nigdy nie przetwarza wiadomości, że inne moduły krawędzi IoT opublikować toohello brokera. W związku z tym hello wdrożenia wywołania zwrotnego wiadomość hello w Witaj Witaj\_moduł world jest funkcją zerowa.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Publikowanie i przetwarzanie komunikatu przez moduł rejestratora

Moduł rejestratora Hello odbiera komunikaty z brokera hello i zapisuje je w pliku tooa. Nigdy nie publikuje żadnych komunikatów. W związku z tym hello kodu modułu rejestratora hello nigdy nie wywołuje hello **Broker_Publish** funkcji.

Witaj **Logger_Receive** funkcji w hello [logger.c] [ lnk-logger-c] plik jest hello wywołania zwrotnego hello brokera wywołuje toodeliver wiadomości toohello rejestratora modułu. Witaj poniższy fragment kodu przedstawia zmienionej wersji z komentarze dodane i obsługi usunięte czytelność kodu niektórych błędów:

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

## <a name="next-steps"></a>Następne kroki

W tym artykule został uruchomiony proste brama brzegowa IoT, który zapisuje plik dziennika tooa wiadomości. toorun przykład, który wysyła wiadomości tooIoT Centrum, zobacz [krawędzi IoT — wysyłanie wiadomości urządzenia do chmury z symulowane urządzenie przy użyciu systemu Linux] [ lnk-gateway-simulated-linux] lub [krawędzi IoT — wysyłać z urządzenia do chmury Symulowane urządzenie przy użyciu systemu Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md