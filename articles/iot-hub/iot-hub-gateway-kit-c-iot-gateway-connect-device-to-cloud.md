---
title: "Użyj bramy IoT połączenia z urządzeniem z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać Intel NUC jako brama IoT łączenia Sensor tag analizy czasowej oraz wysyłania danych czujnika do Centrum IoT Azure w chmurze."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Brama iot Podłącz urządzenie do chmury"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 4fb77ed0241d15338c2574fd22828507c3e40cb3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-to-connect-things-to-the-cloud---sensortag-to-azure-iot-hub"></a><span data-ttu-id="d72da-104">Użyj bramy IoT nawiązać rzeczy cloud - Sensor tag do Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="d72da-104">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="d72da-105">Przed rozpoczęciem tego samouczka, upewnij się, przeprowadzisz [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span><span class="sxs-lookup"><span data-stu-id="d72da-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="d72da-106">W [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), skonfiguruj urządzenie Intel NUC jako brama IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up the Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d72da-107">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d72da-107">What you will learn</span></span>

<span data-ttu-id="d72da-108">Sposób łączenia Texas Instruments Sensor tag (CC2650STK) z Centrum IoT Azure za pomocą bramy IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-108">You learn how to use an IoT gateway to connect a Texas Instruments SensorTag (CC2650STK) to Azure IoT Hub.</span></span> <span data-ttu-id="d72da-109">Brama IoT wysyła temperatury i wilgotności dane zbierane z Sensor tag do Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="d72da-109">The IoT gateway sends temperature and humidity data collected from the SensorTag to Azure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d72da-110">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="d72da-110">What you will do</span></span>

- <span data-ttu-id="d72da-111">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-111">Create an IoT hub.</span></span>
- <span data-ttu-id="d72da-112">Zarejestruj urządzenie w Centrum IoT dla Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-112">Register a device in the IoT hub for the SensorTag.</span></span>
- <span data-ttu-id="d72da-113">Włącz połączenie między bramą IoT i Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-113">Enable the connection between the IoT gateway and the SensorTag.</span></span>
- <span data-ttu-id="d72da-114">Uruchom przykładową aplikację cz wysyłać dane Sensor tag do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-114">Run a BLE sample application to send SensorTag data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d72da-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="d72da-115">What you need</span></span>

- <span data-ttu-id="d72da-116">Samouczek [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) zakończone, w której skonfigurowaniu NUC Intel jako brama IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="d72da-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d72da-117">An active Azure subscription.</span></span> <span data-ttu-id="d72da-118">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d72da-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="d72da-119">Klient SSH, który jest uruchamiany na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="d72da-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="d72da-120">PuTTY jest zalecane w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="d72da-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="d72da-121">Linux i macOS już dostarczane za pomocą klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="d72da-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="d72da-122">Adres IP i nazwy użytkownika i hasło, aby uzyskać dostęp do bramy z klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="d72da-122">The IP address and the username and password to access the gateway from the SSH client.</span></span>
- <span data-ttu-id="d72da-123">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="d72da-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="d72da-124">Tutaj możesz zarejestrować to nowe urządzenie dla użytkownika Sensor tag</span><span class="sxs-lookup"><span data-stu-id="d72da-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-the-connection-between-the-iot-gateway-and-the-sensortag"></a><span data-ttu-id="d72da-125">Włącz połączenie między bramą IoT i Sensor tag</span><span class="sxs-lookup"><span data-stu-id="d72da-125">Enable the connection between the IoT gateway and the SensorTag</span></span>

<span data-ttu-id="d72da-126">W tej sekcji należy wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d72da-126">In this section, you perform the following tasks:</span></span>

- <span data-ttu-id="d72da-127">Pobierz adres MAC Sensor tag dla połączenia Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="d72da-127">Get the MAC address of the SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="d72da-128">Inicjowanie połączenia Bluetooth z bramy IoT do Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-128">Initiate a Bluetooth connection from the IoT gateway to the SensorTag.</span></span>

### <a name="get-the-mac-address-of-the-sensortag-for-bluetooth-connection"></a><span data-ttu-id="d72da-129">Pobierz adres MAC Sensor tag połączenia Bluetooth</span><span class="sxs-lookup"><span data-stu-id="d72da-129">Get the MAC address of the SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="d72da-130">Na komputerze hosta z klientem SSH i połączyć się z bramą IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-130">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="d72da-131">Odblokuj Bluetooth, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-131">Unblock Bluetooth by running the following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="d72da-132">Uruchom usługę Bluetooth na bramie IoT i wprowadź powłoki Bluetooth, aby konfigurować funkcję Bluetooth, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d72da-132">Start the Bluetooth service on the IoT gateway and enter a Bluetooth shell to configure Bluetooth by running the following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="d72da-133">Włącz kontrolera Bluetooth, uruchamiając następujące polecenie w powłoce Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="d72da-133">Power on the Bluetooth controller by running the following command at the Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![Włącz kontrolera Bluetooth na bramie IoT z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="d72da-135">Uruchom skanowanie w poszukiwaniu pobliskimi urządzeniami Bluetooth, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-135">Start scanning for nearby Bluetooth devices by running the following command:</span></span>

   ```bash
   scan on
   ```

   ![Skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="d72da-137">Naciśnij przycisk parowania na Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-137">Press the pairing button on the SensorTag.</span></span> <span data-ttu-id="d72da-138">Zielony PRZEPROWADZONY na błysków Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-138">The green LED on the SensorTag flashes.</span></span>
1. <span data-ttu-id="d72da-139">W powłoce Bluetooth powinien pojawić się Sensor tag został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="d72da-139">At the Bluetooth shell, you should see the SensorTag is found.</span></span> <span data-ttu-id="d72da-140">Zanotuj adres MAC Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="d72da-140">Make a note of the MAC address of the SensorTag.</span></span> <span data-ttu-id="d72da-141">W tym przykładzie jest to adres MAC Sensor tag `24:71:89:C0:7F:82`.</span><span class="sxs-lookup"><span data-stu-id="d72da-141">In this example, the MAC address of the SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="d72da-142">Wyłącz skanowanie za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d72da-142">Turn off the scan by running the following command:</span></span>

   ```bash
   scan off
   ```

   ![Zatrzymuje skanowanie w pobliżu urządzenia Bluetooth z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-the-iot-gateway-to-the-sensortag"></a><span data-ttu-id="d72da-144">Inicjowanie połączenia Bluetooth z bramy IoT do Sensor tag</span><span class="sxs-lookup"><span data-stu-id="d72da-144">Initiate a Bluetooth connection from the IoT gateway to the SensorTag</span></span>

1. <span data-ttu-id="d72da-145">Podłącz do Sensor tag, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-145">Connect to the SensorTag by running the following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Nawiązać Sensor tag z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="d72da-147">Odłącz od Sensor tag, a Wyjdź z powłoki Bluetooth, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d72da-147">Disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Odłącz od Sensor tag z bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="d72da-149">Pomyślnie włączono połączenie między Sensor tag, a brama IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-149">You've successfully enabled the connection between the SensorTag and the IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-to-send-sensortag-data-to-your-iot-hub"></a><span data-ttu-id="d72da-150">Uruchom przykładową aplikację cz wysyłać dane Sensor tag do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="d72da-150">Run a BLE sample application to send SensorTag data to your IoT hub</span></span>

<span data-ttu-id="d72da-151">Przykładowa aplikacja energii małej Bluetooth (cz) są udostępniane przez Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d72da-151">The Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="d72da-152">Przykładowa aplikacja zbiera dane z połączenia cz i wysyłać dane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-152">The sample application collects data from BLE connection and send the data to you IoT hub.</span></span> <span data-ttu-id="d72da-153">Aby uruchomić przykładową aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="d72da-153">To run the sample application, you need to:</span></span>

1. <span data-ttu-id="d72da-154">Konfigurowanie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d72da-154">Configure the sample application.</span></span>
1. <span data-ttu-id="d72da-155">Uruchom przykładową aplikację w bramie IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-155">Run the sample application on the IoT gateway.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="d72da-156">Konfigurowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d72da-156">Configure the sample application</span></span>

1. <span data-ttu-id="d72da-157">Przejdź do folderu przykładowej aplikacji, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-157">Go to the folder of the sample application by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="d72da-158">Otwórz plik konfiguracyjny, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-158">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="d72da-159">Wypełnij następujące wartości w pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d72da-159">In the configuration file, fill in the following values:</span></span>

   <span data-ttu-id="d72da-160">**IoTHubName**: Nazwa centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-160">**IoTHubName**: The name of your IoT hub.</span></span>

   <span data-ttu-id="d72da-161">**IoTHubSuffix**: Pobierz IoTHubSuffix z klucza podstawowego ciąg połączenia urządzenia zanotowaną w dół.</span><span class="sxs-lookup"><span data-stu-id="d72da-161">**IoTHubSuffix**: Get IoTHubSuffix from the primary key of the device connection string that you noted down.</span></span> <span data-ttu-id="d72da-162">Upewnij się, że uzyskać klucz podstawowy ciąg połączenia urządzenia nie klucz podstawowy parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-162">Ensure that you get the primary key of the device connection string, not the primary key of your IoT hub connection string.</span></span> <span data-ttu-id="d72da-163">Klucz podstawowy urządzenia ciągu połączenia jest w formacie `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span><span class="sxs-lookup"><span data-stu-id="d72da-163">The primary key of the device connection string is in the format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="d72da-164">**Transport**: wartość domyślna to `amqp`.</span><span class="sxs-lookup"><span data-stu-id="d72da-164">**Transport**: The default value is `amqp`.</span></span> <span data-ttu-id="d72da-165">Ta wartość przedstawia protokołu podczas transpotation.</span><span class="sxs-lookup"><span data-stu-id="d72da-165">This value shows the protocol during transpotation.</span></span> <span data-ttu-id="d72da-166">Może to być `http`, `amqp`, lub `mqtt`.</span><span class="sxs-lookup"><span data-stu-id="d72da-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="d72da-167">**macAddress**: adres MAC Sensor tag, zanotowaną w dół.</span><span class="sxs-lookup"><span data-stu-id="d72da-167">**macAddress**: The MAC address of the SensorTag that you noted down.</span></span>

   <span data-ttu-id="d72da-168">**deviceID**: identyfikator urządzenia, który został utworzony w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d72da-168">**deviceID**: ID of the device that you created in your IoT hub.</span></span>

   <span data-ttu-id="d72da-169">**deviceKey**: klucz podstawowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d72da-169">**deviceKey**: The primary key of the device connection string.</span></span>

   ![Zakończenie pliku konfiguracji cz przykładowej aplikacji](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="d72da-171">Naciśnij klawisz `ESC` i typ `:wq` można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="d72da-171">Press `ESC` and type `:wq` to save the file.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="d72da-172">Uruchom przykładową aplikację</span><span class="sxs-lookup"><span data-stu-id="d72da-172">Run the sample application</span></span>

1. <span data-ttu-id="d72da-173">Upewnij się, że Sensor tag jest włączona.</span><span class="sxs-lookup"><span data-stu-id="d72da-173">Make sure the SensorTag is powered on.</span></span>
1. <span data-ttu-id="d72da-174">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d72da-174">Run the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="d72da-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d72da-175">Next steps</span></span>

[<span data-ttu-id="d72da-176">Użyj bramy IoT dla transformacji danych czujnika z krawędzią IoT Azure</span><span class="sxs-lookup"><span data-stu-id="d72da-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
