---
title: "Połączenie bramy do pakiet IoT Azure przy użyciu NUC Intel | Dokumentacja firmy Microsoft"
description: "Za pomocą zestawu Microsoft IoT komercyjnych bramy i monitorowania zdalnego wstępnie skonfigurowane rozwiązanie. Użyj brama brzegowa IoT Azure, aby włączyć urządzenia Sensor tag nawiązać połączenie zdalne rozwiązanie monitorowania, wysyłania danych telemetrycznych do chmury i odpowiadać metody wywoływane z poziomu pulpitu nawigacyjnego rozwiązania."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: bda16be1094276fcecef1e708f9d7db307d94a89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-azure-iot-edge-gateway-to-the-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="bcd6e-104">Połączenie bramy Azure IoT krawędzi zdalnego wstępnie skonfigurowane rozwiązanie monitorowania i wysłać dane telemetryczne z Sensor tag</span><span class="sxs-lookup"><span data-stu-id="bcd6e-104">Connect your Azure IoT Edge gateway to the remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="bcd6e-105">Ten samouczek pokazuje, jak na potrzeby wysyłania danych temperatury i wilgotności z urządzeń Sensor tag do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-105">This tutorial shows you how to use Azure IoT Edge to send temperature and humidity data from SensorTag device to the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="bcd6e-106">Sensor tag nawiązanie połączenia bramy Intel NUC pomocą Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-106">The SensorTag connects to the Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="bcd6e-107">W samouczku:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-107">The tutorial uses:</span></span>

- <span data-ttu-id="bcd6e-108">Azure IoT krawędzi do wdrożenia bramy próbki.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-108">Azure IoT Edge to implement a sample gateway.</span></span>
- <span data-ttu-id="bcd6e-109">Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-109">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="bcd6e-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bcd6e-110">Overview</span></span>

<span data-ttu-id="bcd6e-111">W tym samouczku zostaną wykonane następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-111">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="bcd6e-112">Wdrożenie wystąpienia programu zdalnego wstępnie skonfigurowane rozwiązanie monitorowania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-112">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="bcd6e-113">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="bcd6e-114">Skonfiguruj urządzenie bramy Intel NUC do komunikowania się z komputerem i zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-114">Set up your Intel NUC gateway device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="bcd6e-115">Konfigurowanie bramy Intel NUC odbierać dane telemetryczne z urządzeń Sensor tag, a następnie wyślij je do zdalnego pulpitu nawigacyjnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-115">Set up your Intel NUC gateway to receive telemetry from a SensorTag device and send it to the remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="bcd6e-116">[Texas Instruments Sensor tag cz][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="bcd6e-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="bcd6e-117">W tym samouczku pobiera dane telemetryczne przez sieć Bluetooth na urządzeniu Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-117">This tutorial retrieves telemetry data over Bluetooth from the SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="bcd6e-118">Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-118">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="bcd6e-119">Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-119">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="bcd6e-120">Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-120">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="bcd6e-121">Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-121">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="bcd6e-122">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="bcd6e-122">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="bcd6e-123">Konfiguracja połączenia Bluetooth</span><span class="sxs-lookup"><span data-stu-id="bcd6e-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="bcd6e-124">Konfigurować funkcję Bluetooth na NUC firmy Intel, aby włączyć w urządzeniu Sensor tag do łączenia i wysyłania danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-124">Configure Bluetooth on the Intel NUC to enable the SensorTag device to connect and send telemetry.</span></span>

### <a name="find-the-mac-address-of-the-sensortag"></a><span data-ttu-id="bcd6e-125">Znajdź adres MAC Sensor tag</span><span class="sxs-lookup"><span data-stu-id="bcd6e-125">Find the MAC address of the SensorTag</span></span>

1. <span data-ttu-id="bcd6e-126">W powłoce NUC firmy Intel uruchom następujące polecenie, aby odblokować usługa Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-126">In the shell on the Intel NUC, run the following command to unblock the Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="bcd6e-127">Uruchom następujące polecenia, aby uruchomić usługę Bluetooth na NUC firmy Intel, a następnie wprowadź powłoki Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-127">Run the following commands to start the Bluetooth service on the Intel NUC and enter the Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="bcd6e-128">Uruchom następujące polecenie do potęgi na kontrolerze Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-128">Run the following command to power on the Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="bcd6e-129">Jeśli kontroler jest włączona, zostanie wyświetlony komunikat z **Zmienianie zasilania w zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-129">When the controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="bcd6e-130">Uruchom następujące polecenie, aby skanowanie w poszukiwaniu pobliskimi urządzeniami Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-130">Run the following command to scan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="bcd6e-131">Naciśnij przycisk zasilania na Sensor tag, aby był wykrywalny.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-131">Press the power button on the SensorTag to make it discoverable.</span></span> <span data-ttu-id="bcd6e-132">Zielona LED miga.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-132">The green LED flashes.</span></span>

1. <span data-ttu-id="bcd6e-133">Gdy pojawi się komunikat w powłoce, czy kontroler został odnaleziony Sensor tag, zanotuj adres MAC urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-133">When you see a message in the shell that the controller has discovered the SensorTag, make a note of the MAC address of the device.</span></span> <span data-ttu-id="bcd6e-134">Adres MAC wygląda jak **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-134">The MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="bcd6e-135">Należy adres MAC w dalszej części tego samouczka, podczas konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-135">You need the MAC address later in the tutorial when you configure the gateway.</span></span>

1. <span data-ttu-id="bcd6e-136">Uruchom następujące polecenie, aby wyłączyć skanowanie Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-136">Run the following command to turn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="bcd6e-137">Uruchom następujące polecenie, aby sprawdzić, czy można połączyć się z urządzeniem Sensor tag:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-137">Run the following command to verify that you can connect to the SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="bcd6e-138">Jeśli łączysz się pomyślnie, powłoka zawiera komunikat **połączenie przebiegło pomyślnie** i wyświetla informacje o urządzeniu Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-138">If you connect successfully, the shell shows the message **Connection successful** and prints information about the SensorTag device.</span></span> <span data-ttu-id="bcd6e-139">Jeśli nie możesz połączyć wyboru Sensor tag jest nadal włączony.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-139">If you cannot connect, check the SensorTag is still powered on.</span></span>

1. <span data-ttu-id="bcd6e-140">Teraz możesz odłączyć Sensor tag i wyjdź z powłoki Bluetooth, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-140">You can now disconnect from the SensorTag and exit the Bluetooth shell by running the following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-the-custom-iot-edge-module"></a><span data-ttu-id="bcd6e-141">Utworzenie niestandardowego modułu krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="bcd6e-141">Build the custom IoT Edge module</span></span>

<span data-ttu-id="bcd6e-142">Teraz można tworzyć niestandardowe moduł IoT krawędzi, który umożliwia bramy do wysyłania komunikatów do zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-142">You can now build the custom IoT Edge module that enables the gateway to send messages to the remote monitoring solution.</span></span> <span data-ttu-id="bcd6e-143">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="bcd6e-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="bcd6e-144">Pobierz kod źródłowy niestandardowe moduły krawędzi IoT z serwisu GitHub, za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-144">Download the source code for the custom IoT Edge modules from GitHub using the following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="bcd6e-145">Tworzenie niestandardowego modułu krawędzi IoT przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-145">Build the custom IoT Edge module using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="bcd6e-146">Skrypt kompilacji umieszcza niestandardowego modułu krawędzi IoT libsensor2remotemonitoring.so w folderze kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-146">The build script places the libsensor2remotemonitoring.so custom IoT Edge module in the build folder.</span></span>

## <a name="configure-and-run-the-iot-edge-gateway"></a><span data-ttu-id="bcd6e-147">Konfigurowanie i uruchamianie brama brzegowa IoT</span><span class="sxs-lookup"><span data-stu-id="bcd6e-147">Configure and run the IoT Edge gateway</span></span>

<span data-ttu-id="bcd6e-148">Można teraz skonfigurować bramę brzegową IoT, aby wysłać dane telemetryczne z urządzenia Sensor tag do zdalnego pulpitu nawigacyjnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-148">You can now configure the IoT Edge gateway to send telemetry from your SensorTag device to your remote monitoring dashboard.</span></span> <span data-ttu-id="bcd6e-149">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="bcd6e-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="bcd6e-150">W tym samouczku, Użyj standardowego `vi` Edytor tekstu na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-150">In this tutorial, you use the standard `vi` text editor on the Intel NUC.</span></span> <span data-ttu-id="bcd6e-151">Jeśli nie używasz `vi` przed, należy wykonać Samouczek wprowadzający, takich jak [Unix - vi samouczek edytora] [ lnk-vi-tutorial] zapoznać się z tego edytora.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - The vi Editor Tutorial][lnk-vi-tutorial] to familiarize yourself with this editor.</span></span> <span data-ttu-id="bcd6e-152">Alternatywnie możesz zainstalować użytkownikom większy komfort [nano](https://www.nano-editor.org/) edytora za pomocą polecenia `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-152">Alternatively, you can install the more user-friendly [nano](https://www.nano-editor.org/) editor using the command `smart install nano -y`.</span></span>

<span data-ttu-id="bcd6e-153">Otwórz przykładowy plik konfiguracji w **vi** edytora za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-153">Open the sample configuration file in the **vi** editor using the following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="bcd6e-154">W konfiguracji modułu z Centrum IoTHub Znajdź następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-154">Locate the following lines in the configuration for the IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="bcd6e-155">Zastąp symbole zastępcze informacji Centrum IoT utworzony i zapisany na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-155">Replace the placeholder values with the IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="bcd6e-156">Wartość IoTHubName wygląda jak **yourrmsolution37e08**, i wartość IoTSuffix jest zwykle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-156">The value for IoTHubName looks like **yourrmsolution37e08**, and the value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="bcd6e-157">W konfiguracji modułu mapowania Znajdź następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-157">Locate the following lines in the configuration for the mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="bcd6e-158">Zastąp **macAddress** symbol zastępczy adres MAC z Sensor tag zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-158">Replace the **macAddress** placeholder with the MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="bcd6e-159">Zastąp **deviceID** i **deviceKey** symbole zastępcze z identyfikatorów i klucze dla urządzeń wcześniej utworzony w zdalnym rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-159">Replace the **deviceID** and **deviceKey** placeholders with the IDs and keys for the two devices you created in the remote monitoring solution previously.</span></span>

<span data-ttu-id="bcd6e-160">W konfiguracji modułu Sensor tag Znajdź następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-160">Locate the following lines in the configuration for the SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="bcd6e-161">Zastąp **urządzenia\_mac\_adres** symbol zastępczy adres MAC z Sensor tag zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-161">Replace the **device\_mac\_address** placeholder  with the MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="bcd6e-162">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-162">Save your changes.</span></span>

<span data-ttu-id="bcd6e-163">Teraz możesz uruchomić bramę przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-163">You can now run the gateway using the following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="bcd6e-164">Brama brzegowa IoT rozpoczyna się Intel NUC i wysyła dane telemetryczne z Sensor tag do zdalnego rozwiązanie monitorowania:</span><span class="sxs-lookup"><span data-stu-id="bcd6e-164">The IoT Edge gateway starts on the Intel NUC and sends telemetry from the SensorTag to the remote monitoring solution:</span></span>

![Brama brzegowa IoT wysyła dane telemetryczne z Sensor tag][img-telemetry]

<span data-ttu-id="bcd6e-166">Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-166">Press **Ctrl-C** to exit the program at any time.</span></span>

## <a name="view-the-telemetry"></a><span data-ttu-id="bcd6e-167">Widok telemetrii</span><span class="sxs-lookup"><span data-stu-id="bcd6e-167">View the telemetry</span></span>

<span data-ttu-id="bcd6e-168">Brama jest teraz wysyłanie danych telemetrycznych z urządzeń Sensor tag do zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-168">The gateway is now sending telemetry from the SensorTag device to the remote monitoring solution.</span></span> <span data-ttu-id="bcd6e-169">Można wyświetlić dane telemetryczne na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-169">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="bcd6e-170">Polecenia można również wysłać do urządzenia Sensor tag za pośrednictwem bramy z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-170">You can also send commands to your SensorTag device through the gateway from the solution dashboard.</span></span>

- <span data-ttu-id="bcd6e-171">Przejdź do pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-171">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="bcd6e-172">Wybierz urządzenie, skonfigurowane w bramy, która reprezentuje Sensor tag w **urządzenia do widoku** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-172">Select the device you configured in the gateway that represents the SensorTag in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="bcd6e-173">Dane telemetryczne z urządzeń Sensor tag wyświetla na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-173">The telemetry from the SensorTag device displays on the dashboard.</span></span>

![Wyświetl dane telemetryczne z urządzeń Sensor tag][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="bcd6e-175">Pozostawienie zdalnego monitorowania działającej na koncie Azure są rozliczane dla przy uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-175">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="bcd6e-176">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="bcd6e-176">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="bcd6e-177">Usuwanie wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-177">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcd6e-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcd6e-178">Next steps</span></span>

<span data-ttu-id="bcd6e-179">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="bcd6e-179">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started