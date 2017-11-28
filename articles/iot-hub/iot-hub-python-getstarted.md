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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="d21e8-104">Połącz z Centrum IoT tooyour symulowane urządzenie przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="d21e8-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d21e8-105">Na końcu hello tego samouczka masz dwie aplikacje Python:</span><span class="sxs-lookup"><span data-stu-id="d21e8-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="d21e8-106">**CreateDeviceIdentity.py**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacji symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d21e8-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="d21e8-107">**SimulatedDevice.py**, który łączy z tożsamości urządzenia hello utworzony wcześniej tooyour Centrum IoT i okresowo wysyła dane telemetryczne wiadomości przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d21e8-108">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d21e8-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d21e8-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d21e8-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d21e8-110">[Środowisko Python 2.x lub 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="d21e8-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="d21e8-111">Upewnij się, że toouse hello 32-bitowy lub 64-bitowej instalacji co jest wymagane przez konfigurację.</span><span class="sxs-lookup"><span data-stu-id="d21e8-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="d21e8-112">Po wyświetleniu monitu podczas instalacji hello, upewnij się, że zmienna środowiskowa specyficzne dla platformy tooyour tooadd języka Python.</span><span class="sxs-lookup"><span data-stu-id="d21e8-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="d21e8-113">Jeśli używasz języka Python 2.x, może być konieczne zbyt[instalacji lub uaktualnienia *pip*, hello Python pakietu systemu zarządzania][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="d21e8-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="d21e8-114">Jeśli używasz systemu operacyjnego Windows, następnie [pakietu redystrybucyjnego Visual C++] [ lnk-visual-c-redist] tooallow hello stosowania natywnych bibliotek DLL z języka Python.</span><span class="sxs-lookup"><span data-stu-id="d21e8-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="d21e8-115">[Środowisko Node.js 4.0 lub nowsze][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="d21e8-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="d21e8-116">Upewnij się, że toouse hello 32-bitowy lub 64-bitowej instalacji co jest wymagane przez konfigurację.</span><span class="sxs-lookup"><span data-stu-id="d21e8-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="d21e8-117">Jest to wymagane tooinstall hello [narzędzia Explorer Centrum IoT][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="d21e8-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="d21e8-118">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d21e8-118">An active Azure account.</span></span> <span data-ttu-id="d21e8-119">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d21e8-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="d21e8-120">Witaj *pip* pakietami `azure-iothub-service-client` i `azure-iothub-device-client` są obecnie dostępne tylko dla systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="d21e8-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="d21e8-121">Linux/Mac OS można znaleźć w sekcjach systemu Linux i specyficznych dla komputerów Mac OS toohello na powitania [przygotowywanie środowiska projektowego dla języka Python] [ lnk-python-devbox] post.</span><span class="sxs-lookup"><span data-stu-id="d21e8-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d21e8-122">Utworzono centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-122">You have now created your IoT hub.</span></span> <span data-ttu-id="d21e8-123">Użyj hello nazwy hosta Centrum IoT i hello parametry połączenia Centrum IoT w hello pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d21e8-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="d21e8-124">Można również łatwo utworzyć Centrum IoT w wierszu polecenia, używając hello Python lub Node.js na podstawie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d21e8-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="d21e8-125">Artykuł Hello [tworzenia Centrum IoT przy użyciu hello Azure CLI 2.0] [ lnk-azure-cli-hub] pokazuje sposób hello toodo Szybkie kroki.</span><span class="sxs-lookup"><span data-stu-id="d21e8-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="d21e8-126">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="d21e8-126">Create a device identity</span></span>
<span data-ttu-id="d21e8-127">Ta sekcja zawiera hello kroki toocreate aplikacji konsoli języka Python, który tworzy tożsamość urządzenia w rejestrze tożsamości hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="d21e8-128">Urządzenie można połączyć tylko tooIoT koncentratora, jeśli zawiera on wpis w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="d21e8-129">Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d21e8-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="d21e8-130">Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d21e8-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="d21e8-131">Otwórz wiersz polecenia i zainstaluj hello **Azure IoT Hub usługi SDK dla języka Python**.</span><span class="sxs-lookup"><span data-stu-id="d21e8-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="d21e8-132">Zamknij wiersz polecenia powitania po zainstalowaniu hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d21e8-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="d21e8-133">Utwórz plik języka Python o nazwie **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="d21e8-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="d21e8-134">Otwórz go w [Python Edytor/IDE w wybranym][lnk-python-ide-list], na przykład Witaj domyślne [BEZCZYNNY][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="d21e8-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="d21e8-135">Dodaj następujące moduły hello wymagane tooimport kodu z zestawu SDK usług hello hello:</span><span class="sxs-lookup"><span data-stu-id="d21e8-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="d21e8-136">Dodaj powitania po kod, zastępując symbol zastępczy hello `[IoTHub Connection String]` z hello ciąg połączenia dla Centrum IoT hello utworzony w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="d21e8-137">Można użyć dowolnej nazwy jako hello `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="d21e8-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="d21e8-138">Dodaj hello następujących funkcji tooprint niektóre informacje o urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="d21e8-139">Dodaj powitania po funkcja toocreate hello identyfikacji urządzenia przy użyciu hello rejestru Menedżera.</span><span class="sxs-lookup"><span data-stu-id="d21e8-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="d21e8-140">Ponadto funkcja main hello należy dodać następujący i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="d21e8-141">W wierszu polecenia hello Uruchom hello **CreateDeviceIdentity.py** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d21e8-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="d21e8-142">Powinny pojawić się symulowane urządzenie hello pobierania utworzony.</span><span class="sxs-lookup"><span data-stu-id="d21e8-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="d21e8-143">Zanotuj hello **deviceId** i hello **primaryKey** tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="d21e8-144">Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d21e8-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Pomyślne utworzenie urządzenia][1]

> [!NOTE]
> <span data-ttu-id="d21e8-146">Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="d21e8-147">Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d21e8-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="d21e8-148">Jeśli aplikacja wymaga toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d21e8-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="d21e8-149">Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="d21e8-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d21e8-150">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="d21e8-150">Create a simulated device app</span></span>
<span data-ttu-id="d21e8-151">Ta sekcja zawiera hello kroki toocreate aplikację konsoli języka Python, symuluje urządzenia i wysyła Centrum IoT tooyour wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d21e8-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="d21e8-152">Otwórz nowy wiersz polecenia i zainstalować hello Azure IoT Hub urządzenia SDK dla języka Python w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="d21e8-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="d21e8-153">Zamknij wiersz polecenia powitania po zakończeniu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="d21e8-154">Utwórz plik o nazwie **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="d21e8-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="d21e8-155">Otwórz ten plik w edytorze języka Python lub w wybranym środowisku IDE (na przykład w środowisku IDLE).</span><span class="sxs-lookup"><span data-stu-id="d21e8-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="d21e8-156">Dodaj hello następujące moduły hello wymagane tooimport kodu z urządzenia hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d21e8-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="d21e8-157">Dodaj następujący hello kodu i Zastąp symbol zastępczy hello `[IoTHub Device Connection String]` z hello parametry połączenia dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="d21e8-158">ciąg połączenia urządzenia Hello jest zwykle w formacie hello `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="d21e8-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="d21e8-159">Użyj hello **deviceId** i **primaryKey** urządzenia hello utworzony w hello poprzedniej sekcji tooreplace hello `<deviceId>` i `<primaryKey>` odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d21e8-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="d21e8-160">Zastąp symbol zastępczy `<hostName>` nazwą hosta centrum IoT. Zwykle jest to wartość `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="d21e8-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="d21e8-161">Dodaj powitania po toodefine kod potwierdzenia wysyłania wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="d21e8-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="d21e8-162">Dodaj powitania od klienta urządzenia hello tooinitialize kodu.</span><span class="sxs-lookup"><span data-stu-id="d21e8-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="d21e8-163">Dodaj następujący hello funkcji tooformat i wysłać wiadomość z Centrum IoT tooyour symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d21e8-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="d21e8-164">Na koniec należy dodać hello funkcja main.</span><span class="sxs-lookup"><span data-stu-id="d21e8-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="d21e8-165">Zapisz i zamknij hello **SimulatedDevice.py** pliku.</span><span class="sxs-lookup"><span data-stu-id="d21e8-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="d21e8-166">Użytkownik jest teraz gotowy toorun tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d21e8-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="d21e8-167">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="d21e8-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d21e8-168">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d21e8-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="d21e8-169">Odbieranie komunikatów z symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="d21e8-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="d21e8-170">komunikaty telemetrii tooreceive z urządzenia, należy toouse [usługi Event Hubs][lnk-event-hubs-overview]-zgodne punktu końcowego udostępnianych przez hello Centrum IoT, która odczytuje wiadomości powitania od urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d21e8-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="d21e8-171">Witaj odczytu [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka, aby uzyskać informacje dotyczące sposobu tooprocess wiadomości z centrów zdarzeń dla punktu końcowego Centrum zdarzeń zgodnych Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="d21e8-172">Usługi Event Hubs nie obsługuje telemetrii w języku Python jeszcze, więc możesz utworzyć [Node.js](iot-hub-node-node-getstarted.md#D2C_node) lub [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Konsola oparta na usłudze Event Hubs komunikaty urządzenia do chmury hello tooread aplikacji z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d21e8-173">Ten samouczek pokazuje, jak używasz hello [narzędzia Explorer Centrum IoT] [ lnk-iot-hub-explorer] tooread komunikaty te urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="d21e8-174">Otwórz wiersz polecenia i zainstaluj hello Explorer Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="d21e8-175">Uruchom następujące polecenie w wierszu polecenia hello hello, monitorowanie toobegin hello wiadomości urządzenia do chmury z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="d21e8-176">Użyj parametrów połączenia Centrum IoT w symbolu zastępczego powitania po `--login`.</span><span class="sxs-lookup"><span data-stu-id="d21e8-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="d21e8-177">Otwórz nowy wiersz polecenia i przejdź toohello katalog zawierający hello **SimulatedDevice.py** pliku.</span><span class="sxs-lookup"><span data-stu-id="d21e8-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="d21e8-178">Uruchom hello **SimulatedDevice.py** pliku, który okresowo wysyła Centrum IoT tooyour danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="d21e8-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="d21e8-179">Obserwować wiadomości powitania urządzenia na wiersz polecenia hello systemem hello Explorer Centrum IoT z poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Komunikaty środowiska Python przesyłane z urządzenia do chmury][2]

## <a name="next-steps"></a><span data-ttu-id="d21e8-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d21e8-181">Next steps</span></span>
<span data-ttu-id="d21e8-182">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d21e8-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d21e8-183">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d21e8-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="d21e8-184">Możesz obserwować hello komunikatów odebranych przez Centrum IoT hello za pomocą narzędzia Eksplorator Centrum IoT hello hello.</span><span class="sxs-lookup"><span data-stu-id="d21e8-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="d21e8-185">tooexplore hello zestaw SDK Python użycia Centrum IoT Azure szczegółowo, odwiedź stronę [tym repozytorium Git Centrum][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="d21e8-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="d21e8-186">tooreview hello komunikatów możliwości hello Azure IoT Hub usługi SDK dla języka Python, możesz pobrać i uruchomić [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="d21e8-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="d21e8-187">Na symulacyjnych po stronie urządzenia przy użyciu hello Azure IoT Hub urządzenia SDK dla języka Python, możesz pobrać i uruchomić hello [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="d21e8-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="d21e8-188">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d21e8-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d21e8-189">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d21e8-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d21e8-190">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="d21e8-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d21e8-191">[Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="d21e8-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d21e8-192">toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d21e8-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
