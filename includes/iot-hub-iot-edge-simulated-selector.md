> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

W tym przewodniku hello [symulowane urządzenie chmury Przekaż przykładowe] pokazano, jak toouse [Azure IoT krawędzi] [ lnk-sdk] toosend telemetrii urządzenia do chmury tooIoT Centrum z symulowane urządzenia.

Przewodnik składa się z następujących elementów:

* **Architektura**: architektury informacji na temat hello [symulowane urządzenie chmury Przekaż przykładowe].
* **Tworzenie i uruchamianie**: hello kroki wymagane toobuild i przykładowa hello wykonywania.

## <a name="architecture"></a>Architektura

Witaj [symulowane urządzenie chmury Przekaż przykładowe] pokazuje, jak toocreate bramy, która wysyła dane telemetryczne z symulowanych Centrum IoT tooan urządzeń. Urządzenie nie może być możliwe tooconnect bezpośrednio tooIoT Centrum ponieważ hello urządzenia:

* Nie używa protokołu komunikacji rozpoznawany przez Centrum IoT.
* Nie jest dostatecznie inteligentny tooremember hello tożsamości przypisane tooit przez Centrum IoT.

Brama brzegowa IoT umożliwia rozwiązanie tych problemów w hello następujące sposoby:

* bramy Hello rozumie hello protokołu używany przez urządzenie hello, odbiera telemetrię urządzenia do chmury z urządzenia hello i przekazuje te tooIoT wiadomości przy użyciu protokołu zrozumiałe hello Centrum IoT Hub.

* Brama Hello mapuje toodevices tożsamości Centrum IoT i działa jako serwer proxy, gdy urządzenie wysyła komunikaty tooIoT koncentratora.

powitania po diagram przedstawia hello główne składniki próbki hello, tym hello modułów krawędzi IoT:

![][1]

Moduły Hello są przekazywane komunikaty bezpośrednio tooeach innych. Moduły Hello publikowania wiadomości tooan wewnętrzny brokera polegającego na dostarczaniu toohello wiadomości powitania innych modułów przy użyciu mechanizmu subskrypcji. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure IoT krawędzi][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Moduł pozyskiwania protokołu

Ten moduł jest hello punkt początkowy dla odbierania danych z urządzeń, za pośrednictwem bramy hello i w chmurze hello. W przykładowym hello modułu hello:

1. Tworzy symulowane temperatury danych. Jeśli używasz urządzenia fizyczne modułu hello odczytuje dane z tych urządzeń fizycznych.
1. Tworzy komunikat.
1. Witaj symulowane temperatury dane są umieszczane w treści wiadomości powitania.
1. Dodaje właściwość fałszywy komunikat toohello adres MAC.
1. Powoduje, że moduł dalej toohello dostępne wiadomość hello w łańcuchu hello.

wywołuje moduł Hello **wprowadzanie protokołu X** hello poprzedni diagram nosi nazwę **symulowane urządzenie** w kodzie źródłowym hello.

### <a name="mac-lt-gt-iot-hub-id-module"></a>Adres MAC &lt;-&gt; moduł identyfikatora usługi IoT Hub

Ten moduł skanowania pod kątem wiadomości, których właściwość adres Mac. W przykładowym hello hello protokołu wprowadzanie moduł dodaje właściwości adresu MAC hello. Jeśli moduł hello znajdzie takich właściwości, dodaje innej właściwości z komunikatem klucza toohello urządzenia IoT Hub. Moduł Hello następnie tworzy moduł dalej toohello dostępne wiadomość hello w łańcuchu hello.

Deweloper Hello konfiguruje mapowanie między adresy MAC i Centrum IoT tożsamości tooassociate hello symulowane urządzeń za pomocą tożsamości urządzenia IoT Hub. Deweloper Hello ręcznie dodaje mapowania hello jako część konfiguracji modułu hello.

> [!NOTE]
> W tym przykładzie adres MAC jest używany jako unikatowy identyfikator urządzenia i jest korelowany z tożsamością urządzenia usługi IoT Hub. Możesz jednak napisać swój własny moduł, który będzie używał innego unikatowego identyfikatora. Na przykład urządzenia może mieć unikatowe numery seryjne lub dane telemetryczne hello mogą obejmować nazwę unikatową urządzenia osadzonego.

### <a name="iot-hub-communication-module"></a>Moduł komunikacyjny usługi IoT Hub

Ten moduł ma komunikatów z Centrum IoT urządzenia właściwości klucza, która została przypisana w poprzednim module hello. Moduł Hello wysyła wiadomość hello koncentratora tooIoT zawartości za pomocą hello protokołu HTTP. HTTP jest jednym z hello zrozumiał trzy protokoły Centrum IoT.

Zamiast otwarcie połączenia dla każdego symulowanego urządzenia, ten moduł otwiera pojedynczego połączenia HTTP z Centrum IoT toohello bramy hello. Moduł Hello następnie multiplexes połączenia ze wszystkich urządzeń hello symulowane za pośrednictwem tego połączenia. Takie podejście umożliwia tooconnect pojedyncza brama wiele większej liczby urządzeń.

## <a name="before-you-get-started"></a>Przed rozpoczęciem

Przed rozpoczęciem pracy należy:

* [Tworzenie Centrum IoT] [ lnk-create-hub] w Twojej subskrypcji platformy Azure, potrzebna hello nazwa Twojej toocomplete Centrum tego przewodnika. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* Dodaj dwa Centrum IoT tooyour urządzeń i zanotuj ich identyfikatorów i klucze urządzenia. Można użyć hello [explorer urządzenia] [ lnk-device-explorer] lub [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia tooadd utworzony w hello Centrum IoT toohello urządzeń poprzedniego kroku i pobieranie ich kluczy.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[symulowane urządzenie chmury Przekaż przykładowe]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md