---
title: "aaaConnect tooAzure bramy pakiet IoT przy użyciu NUC Intel | Dokumentacja firmy Microsoft"
description: "Użyj hello IoT Microsoft komercyjnych Kit bramy i hello zdalnego wstępnie skonfigurowane rozwiązanie monitorowania. Użyj hello Azure IoT krawędzi bramy tooconnect toohello zdalnego rozwiązanie monitorowania, wysłać symulowanych telemetrii toohello chmury, a odpowiedź toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a><span data-ttu-id="77bef-104">Połącz Twoje toohello bramy Azure IoT krawędzi zdalne monitorowanie wstępnie skonfigurowane rozwiązanie i wysłać symulowanych telemetrii</span><span class="sxs-lookup"><span data-stu-id="77bef-104">Connect your Azure IoT Edge gateway toohello remote monitoring preconfigured solution and send simulated telemetry</span></span>

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

<span data-ttu-id="77bef-105">Ten samouczek pokazuje, jak toouse Azure IoT krawędzi toosimulate temperatury i wilgotności danych toosend toohello monitorowania zdalnego wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="77bef-105">This tutorial shows you how toouse Azure IoT Edge toosimulate temperature and humidity data toosend toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="77bef-106">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="77bef-106">hello tutorial uses:</span></span>

- <span data-ttu-id="77bef-107">Azure IoT krawędzi tooimplement bramy próbki.</span><span class="sxs-lookup"><span data-stu-id="77bef-107">Azure IoT Edge tooimplement a sample gateway.</span></span>
- <span data-ttu-id="77bef-108">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="77bef-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="77bef-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="77bef-109">Overview</span></span>

<span data-ttu-id="77bef-110">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="77bef-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="77bef-111">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="77bef-112">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77bef-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="77bef-113">Konfigurowanie toocommunicate urządzenia bramy NUC firmy Intel, tak do komputera i hello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-113">Set up your Intel NUC gateway device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="77bef-114">Skonfiguruj hello dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello symulowane toosend bramy IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="77bef-114">Configure hello IoT Edge gateway toosend simulated telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="77bef-115">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77bef-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="77bef-116">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="77bef-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="77bef-117">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="77bef-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="77bef-118">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="77bef-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="77bef-119">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="77bef-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

<span data-ttu-id="77bef-120">Powtórz poprzednie tooadd kroki hello drugiego urządzenia przy użyciu Identyfikatora urządzenia, takich jak **device02**.</span><span class="sxs-lookup"><span data-stu-id="77bef-120">Repeat hello previous steps tooadd a second device using a Device ID such as **device02**.</span></span> <span data-ttu-id="77bef-121">Przykładowe Hello wysyła dane z dwóch symulowanego urządzenia zdalnego rozwiązanie monitorowania hello bramy toohello.</span><span class="sxs-lookup"><span data-stu-id="77bef-121">hello sample sends data from two simulated devices in hello gateway toohello remote monitoring solution.</span></span>

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a><span data-ttu-id="77bef-122">Utworzenie niestandardowego modułu krawędzi IoT hello</span><span class="sxs-lookup"><span data-stu-id="77bef-122">Build hello custom IoT Edge module</span></span>

<span data-ttu-id="77bef-123">Teraz można tworzyć hello niestandardowych krawędzi IoT moduł, który umożliwia hello bramy toosend wiadomości toohello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-123">You can now build hello custom IoT Edge module that enables hello gateway toosend messages toohello remote monitoring solution.</span></span> <span data-ttu-id="77bef-124">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="77bef-124">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

<span data-ttu-id="77bef-125">Pobierz kod źródłowy hello hello niestandardowe moduły krawędzi IoT z serwisu GitHub, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="77bef-125">Download hello source code for hello custom IoT Edge modules from GitHub using hello following commands:</span></span>

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

<span data-ttu-id="77bef-126">Utworzenie niestandardowego modułu krawędzi IoT hello, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="77bef-126">Build hello custom IoT Edge module using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

<span data-ttu-id="77bef-127">skrypt kompilacji Hello umieszcza niestandardowego modułu krawędzi IoT hello libsimulator.so w folderze kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="77bef-127">hello build script places hello libsimulator.so custom IoT Edge module in hello build folder.</span></span>

## <a name="configure-and-run-hello-iot-edge-gateway"></a><span data-ttu-id="77bef-128">Konfigurowanie i uruchamianie hello brama brzegowa IoT</span><span class="sxs-lookup"><span data-stu-id="77bef-128">Configure and run hello IoT Edge gateway</span></span>

<span data-ttu-id="77bef-129">Można teraz skonfigurować hello krawędzi IoT bramy toosend symulowane telemetrii tooyour zdalnego pulpitu nawigacyjnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-129">You can now configure hello IoT Edge gateway toosend simulated telemetry tooyour remote monitoring dashboard.</span></span> <span data-ttu-id="77bef-130">Aby uzyskać więcej informacji dotyczących konfigurowania bramy i moduły krawędzi IoT, zobacz [pojęcia dotyczące usługi Azure IoT krawędzi][lnk-gateway-concepts].</span><span class="sxs-lookup"><span data-stu-id="77bef-130">For more information about configuring a gateway and IoT Edge modules, see [Azure IoT Edge concepts][lnk-gateway-concepts].</span></span>

> [!TIP]
> <span data-ttu-id="77bef-131">W tym samouczku użyjesz hello standard `vi` Edytor tekstu na powitania Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="77bef-131">In this tutorial, you use hello standard `vi` text editor on hello Intel NUC.</span></span> <span data-ttu-id="77bef-132">Jeśli nie używasz `vi` przed, należy wykonać Samouczek wprowadzający, takich jak [Unix — Witaj vi samouczek edytora] [ lnk-vi-tutorial] toofamiliarize sobie z tego edytora.</span><span class="sxs-lookup"><span data-stu-id="77bef-132">If you have not used `vi` before, you should complete an introductory tutorial, such as [Unix - hello vi Editor Tutorial][lnk-vi-tutorial] toofamiliarize yourself with this editor.</span></span> <span data-ttu-id="77bef-133">Alternatywnie możesz zainstalować hello użytkownikom większy komfort [nano](https://www.nano-editor.org/) edytora za pomocą polecenia hello `smart install nano -y`.</span><span class="sxs-lookup"><span data-stu-id="77bef-133">Alternatively, you can install hello more user-friendly [nano](https://www.nano-editor.org/) editor using hello command `smart install nano -y`.</span></span>

<span data-ttu-id="77bef-134">Otwórz hello przykładowy plik konfiguracyjny w hello **vi** Edytor przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="77bef-134">Open hello sample configuration file in hello **vi** editor using hello following command:</span></span>

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

<span data-ttu-id="77bef-135">Znajdź hello następujące wiersze w konfiguracji hello modułu Centrum IoTHub hello:</span><span class="sxs-lookup"><span data-stu-id="77bef-135">Locate hello following lines in hello configuration for hello IoTHub module:</span></span>

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

<span data-ttu-id="77bef-136">Zastąp symbol zastępczy hello wartości z Centrum IoT informacji utworzony i zapisany pod hello hello start tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="77bef-136">Replace hello placeholder values with hello IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="77bef-137">wartość Hello IoTHubName wygląda jak **yourrmsolution37e08**, i wartość hello IoTSuffix jest zwykle **azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="77bef-137">hello value for IoTHubName looks like **yourrmsolution37e08**, and hello value for IoTSuffix is typically **azure-devices.net**.</span></span>

<span data-ttu-id="77bef-138">Znajdź hello następujące wiersze w konfiguracji hello modułu mapowania hello:</span><span class="sxs-lookup"><span data-stu-id="77bef-138">Locate hello following lines in hello configuration for hello mapping module:</span></span>

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

<span data-ttu-id="77bef-139">Zastąp hello **deviceID** i **deviceKey** symbole zastępcze z identyfikatorów hello i klucze dla urządzeń hello dwa wcześniej utworzony w hello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-139">Replace hello **deviceID** and **deviceKey** placeholders with hello IDs and keys for hello two devices you created in hello remote monitoring solution previously.</span></span>

<span data-ttu-id="77bef-140">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="77bef-140">Save your changes.</span></span>

<span data-ttu-id="77bef-141">Teraz możesz uruchomić powitalne brama brzegowa IoT przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="77bef-141">You can now run hello IoT Edge gateway using hello following commands:</span></span>

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

<span data-ttu-id="77bef-142">Brama Hello rozpoczyna się na powitania Intel NUC i wysyła symulowane telemetrii toohello zdalnego rozwiązanie monitorowania:</span><span class="sxs-lookup"><span data-stu-id="77bef-142">hello gateway starts on hello Intel NUC and sends simulated telemetry toohello remote monitoring solution:</span></span>

![Brama brzegowa IoT generuje symulowane telemetrii][img-simulated telemetry]

<span data-ttu-id="77bef-144">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="77bef-144">Press **Ctrl-C** tooexit hello program at any time.</span></span>

## <a name="view-hello-telemetry"></a><span data-ttu-id="77bef-145">Dane telemetryczne wyświetleń hello</span><span class="sxs-lookup"><span data-stu-id="77bef-145">View hello telemetry</span></span>

<span data-ttu-id="77bef-146">Witaj brama brzegowa IoT teraz wysyła symulowane telemetrii toohello zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="77bef-146">hello IoT Edge gateway is now sending simulated telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="77bef-147">Można wyświetlić dane telemetryczne hello na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="77bef-147">You can view hello telemetry on hello solution dashboard.</span></span>

- <span data-ttu-id="77bef-148">Przejdź toohello pulpit nawigacyjny rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="77bef-148">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="77bef-149">Wybierz jedno z urządzeń hello dwa skonfigurowane w hello bramy w hello **tooView urządzenia** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="77bef-149">Select one of hello two devices you configured in hello gateway in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="77bef-150">Wyświetla Hello telemetrię z urządzeń bramy hello na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="77bef-150">hello telemetry from hello gateway devices displays on hello dashboard.</span></span>

![Wyświetl dane telemetryczne z urządzenia bramy hello symulowane][img-telemetry-display]

> [!WARNING]
> <span data-ttu-id="77bef-152">Pozostawienie zdalne monitorowanie działającej na koncie Azure hello są rozliczane na powitania jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="77bef-152">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="77bef-153">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="77bef-153">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="77bef-154">Usuń hello wstępnie skonfigurowane rozwiązanie z konta platformy Azure po zakończeniu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="77bef-154">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77bef-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77bef-155">Next steps</span></span>

<span data-ttu-id="77bef-156">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="77bef-156">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started