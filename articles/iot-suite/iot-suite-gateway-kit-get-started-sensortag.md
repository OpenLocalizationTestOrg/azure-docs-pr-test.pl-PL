---
title: "aaaConnect tooAzure bramy pakiet IoT przy użyciu NUC Intel | Dokumentacja firmy Microsoft"
description: "Użyj hello IoT Microsoft komercyjnych Kit bramy i hello zdalnego wstępnie skonfigurowane rozwiązanie monitorowania. Użyj hello Azure IoT krawędzi bramy tooenable zdalne monitorowanie rozwiązania toohello tooconnect urządzeń Sensor tag, wysyłania danych telemetrycznych toohello chmury, a odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a><span data-ttu-id="94486-104">Połącz Twoje toohello bramy Azure IoT krawędzi zdalne monitorowanie wstępnie skonfigurowane rozwiązanie i wysłać dane telemetryczne z Sensor tag</span><span class="sxs-lookup"><span data-stu-id="94486-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send telemetry from a SensorTag</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="94486-105">Ten samouczek pokazuje, jak toouse Azure IoT krawędzi danych temperatury i wilgotności toosend z Sensor tag toohello zdalnego monitorowania urządzenia wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="94486-105">This tutorial shows you how toouse Azure IoT Edge toosend temperature and humidity data from SensorTag device toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="94486-106">Witaj Sensor tag łączy toohello Intel NUC bramy przy użyciu funkcji Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="94486-106">hello SensorTag connects toohello Intel NUC gateway using Bluetooth.</span></span> <span data-ttu-id="94486-107">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="94486-107">hello tutorial uses:</span></span>

- <span data-ttu-id="94486-108">Azure IoT krawędzi tooimplement bramy próbki.</span><span class="sxs-lookup"><span data-stu-id="94486-108">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="94486-109">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="94486-109">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="94486-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="94486-110">Overview</span></span>

<span data-ttu-id="94486-111">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="94486-111">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="94486-112">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-112">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="94486-113">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94486-113">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="94486-114">Konfigurowanie toocommunicate urządzenia bramy NUC firmy Intel, tak do komputera i hello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-114">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="94486-115">Konfigurowanie telemetrii tooreceive Intel NUC bramy z urządzeń Sensor tag i wysłać go toohello zdalny pulpit nawigacyjny monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-115">Set up your Intel NUC gateway tooreceive telemetry from a SensorTag device and send it toohello remote monitoring dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

<span data-ttu-id="94486-116">[Texas Instruments Sensor tag cz][lnk-sensortag].</span><span class="sxs-lookup"><span data-stu-id="94486-116">[Texas Instruments BLE SensorTag][lnk-sensortag].</span></span> <span data-ttu-id="94486-117">W tym samouczku pobiera dane telemetryczne z urządzeń Sensor tag hello w przez sieć Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="94486-117">This tutorial retrieves telemetry data over Bluetooth from hello SensorTag device.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="94486-118">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94486-118">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="94486-119">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="94486-119">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="94486-120">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="94486-120">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="94486-121">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="94486-121">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="94486-122">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="94486-122">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a><span data-ttu-id="94486-123">Konfiguracja połączenia Bluetooth</span><span class="sxs-lookup"><span data-stu-id="94486-123">Configure Bluetooth connectivity</span></span>

<span data-ttu-id="94486-124">Konfigurować funkcję Bluetooth na powitania Intel NUC tooenable hello Sensor tag urządzenia tooconnect i wysyłania danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="94486-124">Configure Bluetooth on hello Intel NUC tooenable hello SensorTag device tooconnect and send telemetry.</span></span>

### <a name="find-hello-mac-address-of-hello-sensortag"></a><span data-ttu-id="94486-125">Znajdź adres MAC hello hello Sensor tag</span><span class="sxs-lookup"><span data-stu-id="94486-125">Find hello MAC address of hello SensorTag</span></span>

1. <span data-ttu-id="94486-126">W powłoce hello na powitania Intel NUC Uruchom hello następujące usługi Bluetooth hello toounblock polecenia:</span><span class="sxs-lookup"><span data-stu-id="94486-126">In hello shell on hello Intel NUC, run hello following command toounblock hello Bluetooth service:</span></span>

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. <span data-ttu-id="94486-127">Hello uruchom następujące polecenia usługa Bluetooth hello toostart na powitania NUC firmy Intel, a wprowadź hello Bluetooth powłoki:</span><span class="sxs-lookup"><span data-stu-id="94486-127">Run hello following commands toostart hello Bluetooth service on hello Intel NUC and enter hello Bluetooth shell:</span></span>

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="94486-128">Uruchom następujące polecenie toopower na kontrolerze Bluetooth hello hello:</span><span class="sxs-lookup"><span data-stu-id="94486-128">Run hello following command toopower on hello Bluetooth controller:</span></span>

    ```bash
    power on
    ```

    <span data-ttu-id="94486-129">Jeśli kontroler hello jest włączona, zostanie wyświetlony komunikat z **Zmienianie zasilania w zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="94486-129">When hello controller is on, you see a message **Changing power on succeeded**.</span></span>

1. <span data-ttu-id="94486-130">Uruchom powitania po tooscan polecenia dla w pobliżu urządzenia Bluetooth:</span><span class="sxs-lookup"><span data-stu-id="94486-130">Run hello following command tooscan for nearby Bluetooth devices:</span></span>

    ```bash
    scan on
    ```

1. <span data-ttu-id="94486-131">Naciśnij przycisk zasilania hello znajdującego się na powitania Sensor tag toomake wykrywalny go.</span><span class="sxs-lookup"><span data-stu-id="94486-131">Press hello power button on hello SensorTag toomake it discoverable.</span></span> <span data-ttu-id="94486-132">miga LED Hello zielony.</span><span class="sxs-lookup"><span data-stu-id="94486-132">hello green LED flashes.</span></span>

1. <span data-ttu-id="94486-133">Po wyświetleniu komunikatu w powłoce hello tego kontrolera hello wykrył hello Sensor tag, zanotuj hello adres MAC urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="94486-133">When you see a message in hello shell that hello controller has discovered hello SensorTag, make a note of hello MAC address of hello device.</span></span> <span data-ttu-id="94486-134">wygląda Hello adres MAC **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="94486-134">hello MAC address looks like **A0:E6:F8:B5:F6:00**.</span></span> <span data-ttu-id="94486-135">Należy adres MAC hello później w samouczku hello podczas konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="94486-135">You need hello MAC address later in hello tutorial when you configure hello gateway.</span></span>

1. <span data-ttu-id="94486-136">Uruchom hello następujące polecenia tooturn Wyłącz Bluetooth skanowania:</span><span class="sxs-lookup"><span data-stu-id="94486-136">Run hello following command tooturn off Bluetooth scanning:</span></span>

    ```bash
    scan off
    ```

1. <span data-ttu-id="94486-137">Uruchom następujące polecenie tooverify, że możesz połączyć urządzeń Sensor tag toohello hello:</span><span class="sxs-lookup"><span data-stu-id="94486-137">Run hello following command tooverify that you can connect toohello SensorTag device:</span></span>

    ```bash
    connect <SensorTag MAC address>
    ```

    <span data-ttu-id="94486-138">Jeśli łączysz się pomyślnie, powłoka hello pokazuje wiadomość hello **połączenie przebiegło pomyślnie** i wyświetla informacje o urządzeniu Sensor tag hello.</span><span class="sxs-lookup"><span data-stu-id="94486-138">If you connect successfully, hello shell shows hello message **Connection successful** and prints information about hello SensorTag device.</span></span> <span data-ttu-id="94486-139">Jeśli nie można połączyć, sprawdź powitalne Sensor tag jest nadal włączony.</span><span class="sxs-lookup"><span data-stu-id="94486-139">If you cannot connect, check hello SensorTag is still powered on.</span></span>

1. <span data-ttu-id="94486-140">Teraz można odłączyć od hello Sensor tag i zakończyć hello Bluetooth powłoki, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="94486-140">You can now disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="94486-141">Utworzenie niestandardowego modułu krawędzi IoT hello</span><span class="sxs-lookup"><span data-stu-id="94486-141">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="94486-142">Teraz można tworzyć hello niestandardowych krawędzi IoT moduł, który umożliwia hello bramy toosend wiadomości toohello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-142">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="94486-143">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="94486-143">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="94486-144">Pobierz kod źródłowy hello hello niestandardowe moduły krawędzi IoT z serwisu GitHub, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="94486-144">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="94486-145">Utworzenie niestandardowego modułu krawędzi IoT hello, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="94486-145">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="94486-146">skrypt kompilacji Hello umieszcza niestandardowego modułu krawędzi IoT hello libsensor2remotemonitoring.so w folderze kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="94486-146">hello build script places hello libsensor2remotemonitoring.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="94486-147">Konfigurowanie i uruchamianie hello brama brzegowa IoT</span><span class="sxs-lookup"><span data-stu-id="94486-147">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="94486-148">Można teraz skonfigurować hello telemetrii toosend bramy krawędzi IoT z Twojej tooyour urządzeń Sensor tag zdalny pulpit nawigacyjny monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-148">You can now configure hello IoT Edge gateway toosend telemetry from your SensorTag device tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="94486-149">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="94486-149">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="94486-150">W tym samouczku użyjesz hello standard `vi` Edytor tekstu na powitania Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="94486-150">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="94486-151">Jeśli nie używasz `vi` przed, należy wykonać Samouczek wprowadzający, takich jak [Unix — Witaj vi samouczek edytora] [ lnk-vi-tutorial] toofamiliarize sobie z tego edytora.</span><span class="sxs-lookup"><span data-stu-id="94486-151">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="94486-152">Alternatywnie możesz zainstalować hello użytkownikom większy komfort [nano](https://www.nano-editor.org/) edytora za pomocą polecenia hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="94486-152">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="94486-153">Otwórz hello przykładowy plik konfiguracyjny w hello **vi** Edytor przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="94486-153">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

<span data-ttu-id="94486-154">Znajdź hello następujące wiersze w konfiguracji hello modułu Centrum IoTHub hello:</span><span class="sxs-lookup"><span data-stu-id="94486-154">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="94486-155">Zastąp symbol zastępczy hello wartości z Centrum IoT informacji utworzony i zapisany pod hello hello start tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="94486-155">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="94486-156">wartość Hello IoTHubName wygląda jak **yourrmsolution37e08**, i wartość hello IoTSuffix jest zwykle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="94486-156">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="94486-157">Znajdź hello następujące wiersze w konfiguracji hello modułu mapowania hello:</span><span class="sxs-lookup"><span data-stu-id="94486-157">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="94486-158">Zastąp hello **macAddress** symbol zastępczy hello adres MAC z Sensor tag zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="94486-158">Replace hello **macAddress** placeholder with hello MAC address of your SensorTag you noted previously.</span></span> <span data-ttu-id="94486-159">Zastąp hello **deviceID** i **deviceKey** symbole zastępcze z identyfikatorów hello i klucze dla urządzeń hello dwa wcześniej utworzony w hello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="94486-159">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="94486-160">Znajdź hello następujące wiersze w konfiguracji hello modułu Sensor tag hello:</span><span class="sxs-lookup"><span data-stu-id="94486-160">Locate hello following lines in hello configuration for hello SensorTag module:</span></span>

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

<span data-ttu-id="94486-161">Zastąp hello **urządzenia\_mac\_adres** symbol zastępczy hello adres MAC z Sensor tag zanotowany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="94486-161">Replace hello **device\_mac\_address** placeholder  with hello MAC address of your SensorTag you noted previously.</span></span>

<span data-ttu-id="94486-162">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="94486-162">Save your changes.</span></span>

<span data-ttu-id="94486-163">Teraz możesz uruchomić bramy hello przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="94486-163">You can now run hello gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

<span data-ttu-id="94486-164">Witaj brama brzegowa IoT rozpoczyna się hello Intel NUC i wysyła dane telemetryczne z hello Sensor tag toohello zdalnego rozwiązanie monitorowania:</span><span class="sxs-lookup"><span data-stu-id="94486-164">hello IoT Edge gateway starts on hello Intel NUC and sends telemetry from hello SensorTag toohello remote monitoring solution:</span></span>

![Brama brzegowa IoT wysyła dane telemetryczne z hello Sensor tag][img-telemetry]

<span data-ttu-id="94486-166">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="94486-166">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="94486-167">Dane telemetryczne wyświetleń hello</span><span class="sxs-lookup"><span data-stu-id="94486-167">View hello telemetry</span></span>

<span data-ttu-id="94486-168">Brama Hello teraz wysyła dane telemetryczne z hello zdalnego rozwiązanie monitorowania Sensor tag urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="94486-168">hello gateway is now sending telemetry from hello SensorTag device toohello remote monitoring solution.</span></span> <span data-ttu-id="94486-169">Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="94486-169">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="94486-170">Można również wysłać polecenia tooyour Sensor tag urządzenia za pośrednictwem bramy hello z pulpitu nawigacyjnego rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="94486-170">You can also send commands tooyour SensorTag device through hello gateway from hello solution dashboard.</span></span>

- <span data-ttu-id="94486-171">Przejdź toohello pulpit nawigacyjny rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="94486-171">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="94486-172">Wybierz hello urządzenia skonfigurowane w hello bramy, która reprezentuje hello Sensor tag w hello **tooView urządzenia** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="94486-172">Select hello device you configured in hello gateway that represents hello SensorTag in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="94486-173">Wyświetla Hello telemetrię z urządzeń Sensor tag hello na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="94486-173">hello telemetry from hello SensorTag device displays on hello dashboard.</span></span>

![Wyświetl dane telemetryczne z urządzeń Sensor tag hello][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="94486-175">Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="94486-175">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="94486-176">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="94486-176">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="94486-177">Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="94486-177">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94486-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94486-178">Next steps</span></span>

<span data-ttu-id="94486-179">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="94486-179">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started