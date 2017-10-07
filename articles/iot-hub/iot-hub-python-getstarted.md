---
title: "aaaGet pracę z Centrum IoT Azure (Python) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla języka Python. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Połącz z Centrum IoT tooyour symulowane urządzenie przy użyciu języka Python
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Na końcu hello tego samouczka masz dwie aplikacje Python:

* **CreateDeviceIdentity.py**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.
* **SimulatedDevice.py**, który łączy z tożsamości urządzenia hello utworzony wcześniej tooyour Centrum IoT i okresowo wysyła dane telemetryczne wiadomości przy użyciu protokołu MQTT hello.

> [!NOTE]
> Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.
> 
> 

toocomplete tego samouczka należy hello następujące:

* [Środowisko Python 2.x lub 3.x][lnk-python-download]. Upewnij się, że toouse hello 32-bitowy lub 64-bitowej instalacji co jest wymagane przez konfigurację. Po wyświetleniu monitu podczas instalacji hello, upewnij się, że zmienna środowiskowa specyficzne dla platformy tooyour tooadd języka Python. Jeśli używasz języka Python 2.x, może być konieczne zbyt[instalacji lub uaktualnienia *pip*, hello Python pakietu systemu zarządzania][lnk-install-pip].
* Jeśli używasz systemu operacyjnego Windows, następnie [pakietu redystrybucyjnego Visual C++] [ lnk-visual-c-redist] tooallow hello stosowania natywnych bibliotek DLL z języka Python.
* [Środowisko Node.js 4.0 lub nowsze][lnk-node-download]. Upewnij się, że toouse hello 32-bitowy lub 64-bitowej instalacji co jest wymagane przez konfigurację. Jest to wymagane tooinstall hello [narzędzia Explorer Centrum IoT][lnk-iot-hub-explorer].
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.

> [!NOTE]
> Witaj *pip* pakietami `azure-iothub-service-client` i `azure-iothub-device-client` są obecnie dostępne tylko dla systemu operacyjnego Windows. Linux/Mac OS można znaleźć w sekcjach systemu Linux i specyficznych dla komputerów Mac OS toohello na powitania [przygotowywanie środowiska projektowego dla języka Python] [ lnk-python-devbox] post.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Utworzono centrum IoT. Użyj hello nazwy hosta Centrum IoT i hello parametry połączenia Centrum IoT w hello pozostałej części tego samouczka.

> [!NOTE]
> Można również łatwo utworzyć Centrum IoT w wierszu polecenia, używając hello Python lub Node.js na podstawie wiersza polecenia platformy Azure. Artykuł Hello [tworzenia Centrum IoT przy użyciu hello Azure CLI 2.0] [ lnk-azure-cli-hub] pokazuje sposób hello toodo Szybkie kroki. 
> 

## <a name="create-a-device-identity"></a>Tworzenie tożsamości urządzenia
Ta sekcja zawiera hello kroki toocreate aplikacji konsoli języka Python, który tworzy tożsamość urządzenia w rejestrze tożsamości hello Centrum IoT. Urządzenie można połączyć tylko tooIoT koncentratora, jeśli zawiera on wpis w rejestrze tożsamości hello. Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity]. Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.

1. Otwórz wiersz polecenia i zainstaluj hello **Azure IoT Hub usługi SDK dla języka Python**. Zamknij wiersz polecenia powitania po zainstalowaniu hello zestawu SDK.

    ```
    pip install azure-iothub-service-client
    ```

2. Utwórz plik języka Python o nazwie **CreateDeviceIdentity.py**. Otwórz go w [Python Edytor/IDE w wybranym][lnk-python-ide-list], na przykład Witaj domyślne [BEZCZYNNY][lnk-idle].

3. Dodaj następujące moduły hello wymagane tooimport kodu z zestawu SDK usług hello hello:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Dodaj powitania po kod, zastępując symbol zastępczy hello `[IoTHub Connection String]` z hello ciąg połączenia dla Centrum IoT hello utworzony w poprzedniej sekcji hello. Można użyć dowolnej nazwy jako hello `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Dodaj hello następujących funkcji tooprint niektóre informacje o urządzeniu hello.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Dodaj powitania po funkcja toocreate hello identyfikacji urządzenia przy użyciu hello rejestru Menedżera. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Ponadto funkcja main hello należy dodać następujący i Zapisz plik hello.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. W wierszu polecenia hello Uruchom hello **CreateDeviceIdentity.py** w następujący sposób:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Powinny pojawić się symulowane urządzenie hello pobierania utworzony. Zanotuj hello **deviceId** i hello **primaryKey** tego urządzenia. Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.

    ![Pomyślne utworzenie urządzenia][1]

> [!NOTE]
> Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia. Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń. Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji. Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
Ta sekcja zawiera hello kroki toocreate aplikację konsoli języka Python, symuluje urządzenia i wysyła Centrum IoT tooyour wiadomości urządzenia do chmury.

1. Otwórz nowy wiersz polecenia i zainstalować hello Azure IoT Hub urządzenia SDK dla języka Python w następujący sposób. Zamknij wiersz polecenia powitania po zakończeniu instalacji hello.

    ```
    pip install azure-iothub-device-client
    ```
2. Utwórz plik o nazwie **SimulatedDevice.py**. Otwórz ten plik w edytorze języka Python lub w wybranym środowisku IDE (na przykład w środowisku IDLE).

3. Dodaj hello następujące moduły hello wymagane tooimport kodu z urządzenia hello zestawu SDK.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Dodaj następujący hello kodu i Zastąp symbol zastępczy hello `[IoTHub Device Connection String]` z hello parametry połączenia dla danego urządzenia. ciąg połączenia urządzenia Hello jest zwykle w formacie hello `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Użyj hello **deviceId** i **primaryKey** urządzenia hello utworzony w hello poprzedniej sekcji tooreplace hello `<deviceId>` i `<primaryKey>` odpowiednio. Zastąp symbol zastępczy `<hostName>` nazwą hosta centrum IoT. Zwykle jest to wartość `<IoT hub name>.azure-devices.net`.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Dodaj powitania po toodefine kod potwierdzenia wysyłania wywołania zwrotnego. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Dodaj powitania od klienta urządzenia hello tooinitialize kodu.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Dodaj następujący hello funkcji tooformat i wysłać wiadomość z Centrum IoT tooyour symulowane urządzenie.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Na koniec należy dodać hello funkcja main. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Zapisz i zamknij hello **SimulatedDevice.py** pliku. Użytkownik jest teraz gotowy toorun tej aplikacji.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Odbieranie komunikatów z symulowanego urządzenia
komunikaty telemetrii tooreceive z urządzenia, należy toouse [usługi Event Hubs][lnk-event-hubs-overview]-zgodne punktu końcowego udostępnianych przez hello Centrum IoT, która odczytuje wiadomości powitania od urządzenia do chmury. Witaj odczytu [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka, aby uzyskać informacje dotyczące sposobu tooprocess wiadomości z centrów zdarzeń dla punktu końcowego Centrum zdarzeń zgodnych Centrum IoT. Usługi Event Hubs nie obsługuje telemetrii w języku Python jeszcze, więc możesz utworzyć [Node.js](iot-hub-node-node-getstarted.md#D2C_node) lub [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Konsola oparta na usłudze Event Hubs komunikaty urządzenia do chmury hello tooread aplikacji z Centrum IoT. Ten samouczek pokazuje, jak używasz hello [narzędzia Explorer Centrum IoT] [ lnk-iot-hub-explorer] tooread komunikaty te urządzenia.

1. Otwórz wiersz polecenia i zainstaluj hello Explorer Centrum IoT. 

    ```
    npm install -g iothub-explorer
    ```

2. Uruchom następujące polecenie w wierszu polecenia hello hello, monitorowanie toobegin hello wiadomości urządzenia do chmury z urządzenia. Użyj parametrów połączenia Centrum IoT w symbolu zastępczego powitania po `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Otwórz nowy wiersz polecenia i przejdź toohello katalog zawierający hello **SimulatedDevice.py** pliku.

4. Uruchom hello **SimulatedDevice.py** pliku, który okresowo wysyła Centrum IoT tooyour danych telemetrycznych. 
   
    ```
    python SimulatedDevice.py
    ```
5. Obserwować wiadomości powitania urządzenia na wiersz polecenia hello systemem hello Explorer Centrum IoT z poprzedniej sekcji hello. 

    ![Komunikaty środowiska Python przesyłane z urządzenia do chmury][2]

## <a name="next-steps"></a>Następne kroki
W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT. Możesz obserwować hello komunikatów odebranych przez Centrum IoT hello za pomocą narzędzia Eksplorator Centrum IoT hello hello. 

tooexplore hello zestaw SDK Python użycia Centrum IoT Azure szczegółowo, odwiedź stronę [tym repozytorium Git Centrum][lnk-python-github]. tooreview hello komunikatów możliwości hello Azure IoT Hub usługi SDK dla języka Python, możesz pobrać i uruchomić [iothub_messaging_sample.py][lnk-messaging-sample]. Na symulacyjnych po stronie urządzenia przy użyciu hello Azure IoT Hub urządzenia SDK dla języka Python, możesz pobrać i uruchomić hello [iothub_client_sample.py][lnk-client-sample].

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Łączenie urządzenia][lnk-connect-device]
* [Wprowadzenie do zarządzania urządzeniami][lnk-device-management]
* [Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)

toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
