---
title: "aaaConnect tooAzure Pi malina pakiet IoT przy użyciu środowiska Node.js w usłudze symulowane telemetrii | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj Node.js tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysłać symulowanych telemetrii toohello chmury i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="1d1a1-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysłać symulowanych dane telemetryczne przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d1a1-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="1d1a1-105">Ten samouczek pokazuje, jak hello toouse malina Pi 3 toosimulate temperatury i wilgotności danych toosend toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="1d1a1-106">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-106">hello tutorial uses:</span></span>

- <span data-ttu-id="1d1a1-107">Raspbian OS hello Node.js język programowania i hello zestawu SDK usługi Microsoft Azure IoT dla tooimplement Node.js urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="1d1a1-108">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="1d1a1-109">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="1d1a1-110">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="1d1a1-111">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="1d1a1-112">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="1d1a1-113">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="1d1a1-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="1d1a1-114">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="1d1a1-114">Download and configure hello sample</span></span>

<span data-ttu-id="1d1a1-115">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="1d1a1-116">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d1a1-116">Install Node.js</span></span>

<span data-ttu-id="1d1a1-117">Jeśli jeszcze tego nie zrobiono tego wcześniej, należy zainstalować Node.js na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="1d1a1-118">Witaj IoT SDK dla środowiska Node.js wymaga wersji 0.11.5 Node.js lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-118">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="1d1a1-119">Witaj poniższej procedurze pokazano, jak tooinstall v6.10.2 Node.js na Twoje Pi malina:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-119">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="1d1a1-120">Użyj hello następujące polecenie tooupdate Twojego Pi malina:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-120">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="1d1a1-121">Użyj następującego polecenia toodownload hello Node.js plików binarnych tooyour Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-121">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="1d1a1-122">Użyj hello następujące pliki binarne hello tooinstall polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-122">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="1d1a1-123">Użyj hello następujące polecenie tooverify Node.js v6.10.2 zostały zainstalowane pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-123">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="1d1a1-124">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="1d1a1-124">Clone hello repositories</span></span>

<span data-ttu-id="1d1a1-125">Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-125">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="1d1a1-126">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="1d1a1-126">Update hello device connection string</span></span>

<span data-ttu-id="1d1a1-127">Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-127">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="1d1a1-128">Znajdź wiersz hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-128">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="1d1a1-129">Zastąp symbole zastępcze hello hello urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-129">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="1d1a1-130">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="1d1a1-130">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="1d1a1-131">Uruchom hello próbki</span><span class="sxs-lookup"><span data-stu-id="1d1a1-131">Run hello sample</span></span>

<span data-ttu-id="1d1a1-132">Witaj uruchom następujące polecenia tooinstall hello pakietów wymagań wstępnych dla przykładu hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-132">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="1d1a1-133">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-133">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="1d1a1-134">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-134">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="1d1a1-135">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="1d1a1-135">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="1d1a1-137">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-137">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="1d1a1-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d1a1-138">Next steps</span></span>

<span data-ttu-id="1d1a1-139">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="1d1a1-139">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
