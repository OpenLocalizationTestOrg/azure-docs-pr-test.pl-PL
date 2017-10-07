---
title: "aaaUse tooconnect bramy IoT tooAzure urządzenia IoT Hub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse NUC Intel jako tooconnect bramy IoT Sensor tag analizy czasowej i tooAzure danych czujnika wysyłania Centrum IoT w hello chmury."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Brama iot połączyć toocloud urządzenia"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="568cb-104">Użyj IoT bramy tooconnect rzeczy toohello cloud - tooAzure Sensor tag Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="568cb-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="568cb-105">Przed rozpoczęciem tego samouczka, upewnij się, przeprowadzisz [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="568cb-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="568cb-106">W [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), konfigurowanie urządzenia Intel NUC hello jako bramę IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="568cb-107">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="568cb-107">What you will learn</span></span>

<span data-ttu-id="568cb-108">Dowiesz się, jak toouse tooconnect bramy IoT tooAzure Sensor Texas Instruments tag (CC2650STK) Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="568cb-109">Brama IoT Hello wysyła temperatury i wilgotności dane zbierane z hello Sensor tag tooAzure Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="568cb-110">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="568cb-110">What you will do</span></span>

- <span data-ttu-id="568cb-111">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-111">Create an IoT hub.</span></span>
- <span data-ttu-id="568cb-112">Zarejestruj urządzenie w Centrum IoT hello hello Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="568cb-113">Włącz hello połączenie między bramą IoT hello i hello Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="568cb-114">Uruchom cz przykładowej aplikacji toosend Sensor tag danych tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="568cb-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="568cb-115">What you need</span></span>

- <span data-ttu-id="568cb-116">Samouczek [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) zakończone, w której skonfigurowaniu NUC Intel jako brama IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="568cb-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="568cb-117">An active Azure subscription.</span></span> <span data-ttu-id="568cb-118">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="568cb-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="568cb-119">Klient SSH, który jest uruchamiany na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="568cb-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="568cb-120">PuTTY jest zalecane w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="568cb-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="568cb-121">Linux i macOS już dostarczane za pomocą klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="568cb-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="568cb-122">adres IP Hello i hello nazwy użytkownika i hasła tooaccess hello bramy z powitania klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="568cb-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="568cb-123">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="568cb-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="568cb-124">Tutaj możesz zarejestrować to nowe urządzenie dla użytkownika Sensor tag</span><span class="sxs-lookup"><span data-stu-id="568cb-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="568cb-125">Włącz hello połączenie między bramą IoT hello i hello Sensor tag</span><span class="sxs-lookup"><span data-stu-id="568cb-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="568cb-126">W tej sekcji należy wykonać następujące zadania hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="568cb-127">Pobierz adres MAC hello hello Sensor tag dla połączenia Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="568cb-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="568cb-128">Inicjowanie połączenia Bluetooth z hello IoT bramy toohello Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="568cb-129">Pobierz adres MAC hello hello Sensor tag połączenia Bluetooth</span><span class="sxs-lookup"><span data-stu-id="568cb-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="568cb-130">Na komputerze hosta hello Uruchom klienta SSH hello i połącz toohello IoT bramy.</span><span class="sxs-lookup"><span data-stu-id="568cb-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="568cb-131">Odblokuj Bluetooth, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="568cb-132">Uruchom usługę Bluetooth hello na powitania IoT bramy, a następnie wprowadź tooconfigure powłoki Bluetooth, hello Bluetooth, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="568cb-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="568cb-133">Włącz hello Bluetooth kontrolera, uruchamiając hello następujące polecenia na powitania powłoki Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="568cb-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Włącz hello kontrolera Bluetooth na powitania IoT bramy z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="568cb-135">Uruchom skanowanie w poszukiwaniu w pobliżu urządzenia Bluetooth, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![Skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="568cb-137">Naciśnij klawisz hello parowanie przycisk na powitania Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="568cb-138">zielony Hello PRZEPROWADZONY na powitania błysków Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="568cb-139">Na powitania powłoki Bluetooth powinna zostać wyświetlona hello znalezionych Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="568cb-140">Zanotuj hello adres MAC hello Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="568cb-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="568cb-141">W tym przykładzie hello hello Sensor tag adresu MAC jest `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="568cb-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="568cb-142">Wyłącz skanowanie hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![Zatrzymuje skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="568cb-144">Inicjowanie połączenia Bluetooth z hello IoT bramy toohello Sensor tag</span><span class="sxs-lookup"><span data-stu-id="568cb-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="568cb-145">Połącz toohello Sensor tag, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Połącz z bluetoothctl toohello Sensor tag](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="568cb-147">Odłącz od hello Sensor tag, a następnie zakończyć hello Bluetooth powłoki, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Odłącz od hello Sensor tag z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="568cb-149">Pomyślnie włączono hello połączenie między hello Sensor tag i hello IoT bramy.</span><span class="sxs-lookup"><span data-stu-id="568cb-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="568cb-150">Uruchom cz przykładowej aplikacji toosend Sensor tag danych tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="568cb-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="568cb-151">Energii małej Bluetooth (cz) Przykładowa aplikacja Hello są udostępniane przez Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="568cb-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="568cb-152">Witaj przykładowej aplikacji zbiera dane z połączenia cz i Wyślij Centrum IoT tooyou danych hello.</span><span class="sxs-lookup"><span data-stu-id="568cb-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="568cb-153">toorun hello przykładowej aplikacji, musisz:</span><span class="sxs-lookup"><span data-stu-id="568cb-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="568cb-154">Skonfiguruj hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="568cb-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="568cb-155">Uruchom hello Przykładowa aplikacja hello IoT bramy.</span><span class="sxs-lookup"><span data-stu-id="568cb-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="568cb-156">Skonfiguruj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="568cb-156">Configure hello sample application</span></span>

1. <span data-ttu-id="568cb-157">Folder przejdź toohello hello przykładowej aplikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="568cb-158">Otwórz plik konfiguracji hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="568cb-159">W pliku konfiguracyjnym hello Wypełnij hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="568cb-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="568cb-160">**IoTHubName**: hello nazwę Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="568cb-161">**IoTHubSuffix**: Pobierz IoTHubSuffix z hello klucz podstawowy ciąg połączenia urządzenia hello zanotowaną w dół.</span><span class="sxs-lookup"><span data-stu-id="568cb-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="568cb-162">Upewnij się, możesz pobrać klucz podstawowy hello ciąg połączenia urządzenia hello, nie hello klucz podstawowy parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="568cb-163">klucz podstawowy Hello ciąg połączenia urządzenia hello jest w formacie hello `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="568cb-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="568cb-164">**Transport**: hello wartość domyślna to `amqp`.</span><span class="sxs-lookup"><span data-stu-id="568cb-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="568cb-165">Ta wartość przedstawia hello protokołu podczas transpotation.</span><span class="sxs-lookup"><span data-stu-id="568cb-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="568cb-166">Może to być `http`, `amqp`, lub `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="568cb-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="568cb-167">**macAddress**: hello adres MAC hello Sensor tag zanotowaną w dół.</span><span class="sxs-lookup"><span data-stu-id="568cb-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="568cb-168">**deviceID**: identyfikator urządzenia hello, który został utworzony w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="568cb-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="568cb-169">**deviceKey**: hello klucz podstawowy ciąg połączenia urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="568cb-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Plik konfiguracji pełną hello hello cz przykładowej aplikacji](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="568cb-171">Naciśnij klawisz `ESC` i typ `:wq` toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="568cb-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="568cb-172">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="568cb-172">Run hello sample application</span></span>

1. <span data-ttu-id="568cb-173">Upewnij się, że powitalne Sensor tag jest włączona.</span><span class="sxs-lookup"><span data-stu-id="568cb-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="568cb-174">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="568cb-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="568cb-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="568cb-175">Next steps</span></span>

[<span data-ttu-id="568cb-176">Użyj bramy IoT dla transformacji danych czujnika z krawędzią IoT Azure</span><span class="sxs-lookup"><span data-stu-id="568cb-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
