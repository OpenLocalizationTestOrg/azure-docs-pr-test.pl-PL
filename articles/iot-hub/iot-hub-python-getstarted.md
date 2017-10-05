---
title: "Rozpoczynanie pracy z usługą Azure IoT Hub (Python) | Microsoft Docs"
description: "Dowiedz się, jak wysyłać komunikaty urządzenie-chmura do usługi Azure IoT Hub za pomocą zestawów SDK usługi IoT dla języka Python. Utwórz symulowane aplikacje urządzenia i usługi, aby zarejestrować urządzenie, wysyłać wiadomości i odczytywać wiadomości z usługi IoT Hub."
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
ms.openlocfilehash: 7ebbac4464d793717f68a4cb7905c53d1f5c051a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-python"></a><span data-ttu-id="b932c-104">Podłączanie symulowanego urządzenia do usługi IoT Hub za pomocą języka Python</span><span class="sxs-lookup"><span data-stu-id="b932c-104">Connect your simulated device to your IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="b932c-105">Na koniec tego samouczka będziesz mieć dwie aplikacje Python:</span><span class="sxs-lookup"><span data-stu-id="b932c-105">At the end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="b932c-106">**CreateDeviceIdentity.py**, która tworzy tożsamość urządzenia i skojarzony klucz zabezpieczeń w celu podłączenia symulowanej aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="b932c-107">**SimulatedDevice.py**, która łączy się z usługą IoT Hub przy użyciu utworzonej wcześniej tożsamości urządzenia i okresowo wysyła komunikat telemetrii przy użyciu protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="b932c-107">**SimulatedDevice.py**, which connects to your IoT hub with the device identity created earlier, and periodically sends a telemetry message using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b932c-108">Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK usług Azure IoT) zawiera informacje dotyczące zestawów SDK usług Azure IoT, przy użyciu których można tworzyć aplikacje zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b932c-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b932c-109">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b932c-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b932c-110">[Środowisko Python 2.x lub 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="b932c-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="b932c-111">Upewnij się, że używasz 32-bitowej lub 64-bitowej instalacji zgodnie z wymaganiami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b932c-111">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="b932c-112">Po wyświetleniu monitu podczas instalacji upewnij się, że język Python został dodany do zmiennej środowiskowej specyficznej dla platformy.</span><span class="sxs-lookup"><span data-stu-id="b932c-112">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="b932c-113">Jeśli używasz środowiska Python 2.x, może być konieczne [zainstalowanie lub uaktualnienie systemu zarządzania pakietami języka Python — *pip*][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="b932c-113">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="b932c-114">[Pakiet redystrybucyjny języka Visual C++][lnk-visual-c-redist] (jeśli używasz systemu operacyjnego Windows) umożliwiający korzystanie z natywnych bibliotek DLL języka Python.</span><span class="sxs-lookup"><span data-stu-id="b932c-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="b932c-115">[Środowisko Node.js 4.0 lub nowsze][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="b932c-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="b932c-116">Upewnij się, że używasz 32-bitowej lub 64-bitowej instalacji zgodnie z wymaganiami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b932c-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="b932c-117">Jest to niezbędne do zainstalowania [narzędzia IoT Hub Explorer][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="b932c-117">This is needed to install the [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="b932c-118">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b932c-118">An active Azure account.</span></span> <span data-ttu-id="b932c-119">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b932c-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="b932c-120">Pakiety *pip* dla składników `azure-iothub-service-client` i `azure-iothub-device-client` są obecnie dostępne tylko w przypadku systemu operacyjnego Windows.</span><span class="sxs-lookup"><span data-stu-id="b932c-120">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="b932c-121">W przypadku systemu operacyjnego Linux lub Mac OS zapoznaj się z sekcją poświęconą danemu systemowi w poście [Prepare your development environment for Python][lnk-python-devbox] (Przygotowanie środowiska projektowego dla języka Python).</span><span class="sxs-lookup"><span data-stu-id="b932c-121">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="b932c-122">Utworzono centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-122">You have now created your IoT hub.</span></span> <span data-ttu-id="b932c-123">Użyj tej nazwy hosta usługi IoT Hub oraz jej parametrów połączenia w pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b932c-123">Use the IoT Hub host name and the IoT Hub connection string in the rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="b932c-124">Centrum IoT można również łatwo utworzyć w wierszu polecenia, korzystając z interfejsu wiersza polecenia platformy Azure opartego na środowisku Python lub Node.js.</span><span class="sxs-lookup"><span data-stu-id="b932c-124">You can also easily create your IoT hub on a command line, using the Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="b932c-125">Szybkie kroki wykonania tego zadania zawiera artykuł [Create an IoT hub using the Azure CLI 2.0][lnk-azure-cli-hub] (Tworzenie centrum IoT za pomocą interfejsu wiersza polecenia platformy Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="b932c-125">The article [Create an IoT hub using the Azure CLI 2.0][lnk-azure-cli-hub] shows you the quick steps to do so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="b932c-126">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="b932c-126">Create a device identity</span></span>
<span data-ttu-id="b932c-127">W tej sekcji znajdują się kroki umożliwiające utworzenie aplikacji konsoli języka Python, która tworzy tożsamość urządzenia w rejestrze tożsamości w centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-127">This section lists the steps to create a Python console app, that creates a device identity in the identity registry of your IoT hub.</span></span> <span data-ttu-id="b932c-128">Urządzenie może nawiązać połączenie z usługą IoT Hub tylko wtedy, jeśli ma wpis w rejestrze tożsamości.</span><span class="sxs-lookup"><span data-stu-id="b932c-128">A device can only connect to IoT Hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="b932c-129">Więcej informacji znajduje się w sekcji **Identity registry** (Rejestr tożsamości) artykułu [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="b932c-129">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="b932c-130">Po uruchomieniu ta aplikacja konsoli generuje unikatowy identyfikator urządzenia i klucz, których urządzenie może użyć do zidentyfikowania się podczas wysyłania komunikatów do chmury do usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b932c-130">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="b932c-131">Otwórz wiersz polecenia i zainstaluj **zestaw SDK usługi Azure IoT Hub dla języka Python**.</span><span class="sxs-lookup"><span data-stu-id="b932c-131">Open a command prompt and install the **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="b932c-132">Zamknij wiersz polecenia po zainstalowaniu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="b932c-132">Close the command prompt after you install the SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="b932c-133">Utwórz plik języka Python o nazwie **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="b932c-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="b932c-134">Otwórz go w [edytorze języka Python lub w wybranym środowisku IDE][lnk-python-ide-list], na przykład w domyślnym środowisku [IDLE][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="b932c-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, the default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="b932c-135">Dodaj następujący kod umożliwiający zaimportowanie wymaganych modułów z zestawu SDK usługi:</span><span class="sxs-lookup"><span data-stu-id="b932c-135">Add the following code to import the required modules from the service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="b932c-136">Dodaj następujący kod, zastępując symbol zastępczy `[IoTHub Connection String]` parametrami połączenia centrum IoT utworzonego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b932c-136">Add the following code, replacing the placeholder for `[IoTHub Connection String]` with the connection string for the IoT hub you created in the previous section.</span></span> <span data-ttu-id="b932c-137">Jako identyfikatora `DEVICE_ID` można użyć dowolnej nazwy.</span><span class="sxs-lookup"><span data-stu-id="b932c-137">You can use any name as the `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="b932c-138">Dodaj następującą funkcję umożliwiającą wydrukowanie niektórych informacji o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b932c-138">Add the following function to print some of the device information.</span></span>

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
3. <span data-ttu-id="b932c-139">Dodaj następującą funkcję umożliwiającą utworzenie identyfikacji urządzenia przy użyciu Menedżera rejestru.</span><span class="sxs-lookup"><span data-stu-id="b932c-139">Add the following function to create the device identification using the Registry Manager.</span></span> 

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
4. <span data-ttu-id="b932c-140">Na końcu dodaj funkcję main w przedstawiony sposób i zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="b932c-140">Finally, add the main function as follows and save the file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using the Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="b932c-141">W wierszu polecenia uruchom plik **CreateDeviceIdentity.py** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b932c-141">On the command prompt, run the **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="b932c-142">Powinno zostać wyświetlone utworzone symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="b932c-142">You should see the simulated device getting created.</span></span> <span data-ttu-id="b932c-143">Zanotuj wartości parametrów **deviceId** i **primaryKey** tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-143">Note down the **deviceId** and the **primaryKey** of this device.</span></span> <span data-ttu-id="b932c-144">Te wartości będą potrzebne później podczas tworzenia aplikacji, która łączy się z usługą IoT Hub jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="b932c-144">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

    ![Pomyślne utworzenie urządzenia][1]

> [!NOTE]
> <span data-ttu-id="b932c-146">Rejestr tożsamości usługi IoT Hub przechowuje tożsamości urządzenia tylko po to, aby umożliwić bezpieczny dostęp do centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-146">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="b932c-147">Przechowuje identyfikatory i klucze urządzeń, które będą używane jako poświadczenia zabezpieczeń, oraz flagę włączone/wyłączone, która umożliwia wyłączenie dostępu do poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b932c-147">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="b932c-148">Jeśli aplikacja wymaga przechowywania innych metadanych dla określonego urządzenia, powinna korzystać z magazynu określonego dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b932c-148">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="b932c-149">Więcej informacji znajduje się w temacie [IoT Hub developer guide][lnk-devguide-identity] (Usługa IoT Hub — przewodnik dewelopera).</span><span class="sxs-lookup"><span data-stu-id="b932c-149">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b932c-150">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="b932c-150">Create a simulated device app</span></span>
<span data-ttu-id="b932c-151">Ta sekcja zawiera instrukcje dotyczące tworzenia aplikacji konsoli języka Python, która symuluje urządzenie i wysyła do centrum IoT komunikaty z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="b932c-151">This section lists the steps to create a Python console app, that simulates a device and sends device-to-cloud messages to your IoT hub.</span></span>

1. <span data-ttu-id="b932c-152">Otwórz nowy wiersz polecenia i zainstaluj zestaw SDK urządzenia usługi Azure IoT Hub dla języka Python w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b932c-152">Open a new command prompt and install the Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="b932c-153">Po ukończeniu instalacji zamknij wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-153">Close the command prompt after the installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="b932c-154">Utwórz plik o nazwie **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="b932c-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="b932c-155">Otwórz ten plik w edytorze języka Python lub w wybranym środowisku IDE (na przykład w środowisku IDLE).</span><span class="sxs-lookup"><span data-stu-id="b932c-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="b932c-156">Dodaj następujący kod umożliwiający zaimportowanie wymaganych modułów z zestawu SDK urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-156">Add the following code to import the required modules from the device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="b932c-157">Dodaj następujący kod i zastąp symbol zastępczy `[IoTHub Device Connection String]` parametrami połączenia dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-157">Add the following code and replace the placeholder for `[IoTHub Device Connection String]` with the connection string for your device.</span></span> <span data-ttu-id="b932c-158">Parametry połączenia urządzenia mają zazwyczaj format `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="b932c-158">The device connection string is usually in the format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="b932c-159">Zastąp symbole zastępcze `<deviceId>` i `<primaryKey>` odpowiednio wartościami parametrów **deviceId** i **primaryKey** urządzenia utworzonego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b932c-159">Use the **deviceId** and **primaryKey** of the device you created in the previous section to replace the `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="b932c-160">Zastąp symbol zastępczy `<hostName>` nazwą hosta centrum IoT. Zwykle jest to wartość `<IoT hub name>.azure-devices.net`.</span><span class="sxs-lookup"><span data-stu-id="b932c-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in the format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="b932c-161">Dodaj następujący kod, aby zdefiniować wywołanie zwrotne potwierdzenia wysyłania.</span><span class="sxs-lookup"><span data-stu-id="b932c-161">Add the following code to define a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="b932c-162">Dodaj następujący kod, aby zainicjować klienta urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-162">Add the following code to initialize the device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set the time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="b932c-163">Dodaj następującą funkcję umożliwiającą sformatowanie i wysłanie komunikatu z symulowanego urządzenia do centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-163">Add the following function to format and send a message from your simulated device to your IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C to exit" )
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
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission to IoT Hub." % message_counter )

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
8. <span data-ttu-id="b932c-164">Na koniec dodaj funkcję main.</span><span class="sxs-lookup"><span data-stu-id="b932c-164">Finally, add the main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="b932c-165">Zapisz i zamknij plik **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="b932c-165">Save and close the **SimulatedDevice.py** file.</span></span> <span data-ttu-id="b932c-166">Teraz można przystąpić do uruchomienia tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b932c-166">You are now ready to run this app.</span></span>

> [!NOTE]
> <span data-ttu-id="b932c-167">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="b932c-167">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b932c-168">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="b932c-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="b932c-169">Odbieranie komunikatów z symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="b932c-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="b932c-170">Do odbierania komunikatów telemetrycznych z urządzenia należy użyć [usługi Event Hubs][lnk-event-hubs-overview] — zgodnego punktu końcowego udostępnianego przez usługę IoT Hub, który odczytuje komunikaty wysyłane z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="b932c-170">To receive telemetry messages from your device, you need to use an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by the IoT Hub, which reads the device-to-cloud messages.</span></span> <span data-ttu-id="b932c-171">Przeczytaj samouczek [Get Started with Event Hubs][lnk-eventhubs-tutorial] (Usługa Event Hubs — wprowadzenie), aby uzyskać informacje dotyczące sposobu przetwarzania komunikatów z usługi Event Hubs przeznaczonych dla zgodnego z centrum zdarzeń punktu końcowego centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-171">Read the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how to process messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="b932c-172">Usługa Event Hubs nie obsługuje jeszcze telemetrii w języku Python, można więc utworzyć aplikację konsoli środowiska [Node.js](iot-hub-node-node-getstarted.md#D2C_node) lub [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) opartą na usłudze Event Hubs, która umożliwi odczytywanie komunikatów wysyłanych z urządzenia do chmury pochodzących z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b932c-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app to read the device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="b932c-173">W tym samouczku pokazano, jak skorzystać z [narzędzia IoT Hub Explorer][lnk-iot-hub-explorer] do odczytywania tych komunikatów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b932c-173">This tutorial shows how you can use the [IoT Hub Explorer tool][lnk-iot-hub-explorer] to read these device messages.</span></span>

1. <span data-ttu-id="b932c-174">Otwórz wiersz polecenia i zainstaluj narzędzie IoT Hub Explorer.</span><span class="sxs-lookup"><span data-stu-id="b932c-174">Open a command prompt and install the IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="b932c-175">Uruchom następujące polecenie w wierszu polecenia, aby rozpocząć monitorowanie z urządzenia komunikatów wysyłanych z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="b932c-175">Run the following command on the command prompt, to begin monitoring the device-to-cloud messages from your device.</span></span> <span data-ttu-id="b932c-176">Użyj parametrów połączenia z Twojego centrum IoT w miejsce symbolu zastępczego po `--login`.</span><span class="sxs-lookup"><span data-stu-id="b932c-176">Use your IoT hub's connection string in the placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="b932c-177">Otwórz nowy wiersz polecenia i przejdź do katalogu zawierającego plik **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="b932c-177">Open a new command prompt and navigate to the directory containing the **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="b932c-178">Uruchom plik **SimulatedDevice.py**, który okresowo wysyła dane telemetryczne do Twojego centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-178">Run the **SimulatedDevice.py** file, which periodically sends telemetry data to your IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="b932c-179">W wierszu polecenia z uruchomionym w poprzedniej sekcji narzędziem IoT Hub Explorer obserwuj komunikaty z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b932c-179">Observe the device messages on the command prompt running the IoT Hub Explorer from the previous section.</span></span> 

    ![Komunikaty środowiska Python przesyłane z urządzenia do chmury][2]

## <a name="next-steps"></a><span data-ttu-id="b932c-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b932c-181">Next steps</span></span>
<span data-ttu-id="b932c-182">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="b932c-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="b932c-183">Tożsamość urządzenia została użyta, aby włączyć w aplikacji symulowanego urządzenia funkcję wysyłania komunikatów z urządzenia do chmury do centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b932c-183">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="b932c-184">Z pomocą narzędzia IoT Hub Explorer obserwowano komunikaty odbierane przez centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b932c-184">You observed the messages received by the IoT hub with the help of the IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="b932c-185">Aby szczegółowo przeanalizować możliwości użycia zestawu SDK języka Python dla usługi Azure IoT Hub, odwiedź [to repozytorium GitHub][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="b932c-185">To explore the Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="b932c-186">Aby przejrzeć możliwości obsługi wiadomości zestawu SDK usługi Azure IoT Hub dla języka Python, możesz pobrać i uruchomić plik [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="b932c-186">To review the messaging capabilities of the Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="b932c-187">Aby zapoznać się z możliwościami symulacji ze strony urządzenia przy użyciu zestawu SDK urządzenia usługi Azure IoT Hub dla języka Python, możesz pobrać i uruchomić plik [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="b932c-187">For device side simulation using the Azure IoT Hub Device SDK for Python, you can download and run the [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="b932c-188">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b932c-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b932c-189">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="b932c-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="b932c-190">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="b932c-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="b932c-191">[Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="b932c-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b932c-192">Aby dowiedzieć się, jak rozszerzyć rozwiązanie IoT i przetwarzać komunikaty z urządzenia do chmury na dużą skalę, zobacz samouczek [Przetwarzanie komunikatów przesyłanych z urządzeń do chmury][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="b932c-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
