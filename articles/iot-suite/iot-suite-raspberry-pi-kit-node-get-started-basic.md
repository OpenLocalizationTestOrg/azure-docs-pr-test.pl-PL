---
title: "aaaConnect tooAzure Pi malina pakiet IoT przy użyciu środowiska Node.js w usłudze rzeczywistych czujników | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj Node.js tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a><span data-ttu-id="7b280-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysyłania danych telemetrycznych z czujnika rzeczywistego przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="7b280-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="7b280-105">Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla toodevelop malina Pi 3 czytnik temperatury i wilgotności, który może komunikować się z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="7b280-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="7b280-106">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-106">hello tutorial uses:</span></span>

- <span data-ttu-id="7b280-107">Raspbian OS hello Node.js język programowania i hello zestawu SDK usługi Microsoft Azure IoT dla tooimplement Node.js urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="7b280-107">Raspbian OS, hello Node.js programming language, and hello Microsoft Azure IoT SDK for Node.js tooimplement a sample device.</span></span>
- <span data-ttu-id="7b280-108">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7b280-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="7b280-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7b280-109">Overview</span></span>

<span data-ttu-id="7b280-110">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7b280-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="7b280-111">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="7b280-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="7b280-112">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7b280-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="7b280-113">Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7b280-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="7b280-114">Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="7b280-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="7b280-115">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7b280-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="7b280-116">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7b280-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="7b280-117">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="7b280-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="7b280-118">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="7b280-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="7b280-119">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="7b280-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="7b280-120">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="7b280-120">Download and configure hello sample</span></span>

<span data-ttu-id="7b280-121">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="7b280-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="7b280-122">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="7b280-122">Install Node.js</span></span>

<span data-ttu-id="7b280-123">Zainstaluj środowisko Node.js na Twoje malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="7b280-123">Install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="7b280-124">Witaj IoT SDK dla środowiska Node.js wymaga wersji 0.11.5 Node.js lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7b280-124">hello IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="7b280-125">Witaj poniższej procedurze pokazano, jak tooinstall v6.10.2 Node.js na Twoje Pi malina:</span><span class="sxs-lookup"><span data-stu-id="7b280-125">hello following steps show you how tooinstall Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="7b280-126">Użyj hello następujące polecenie tooupdate Twojego Pi malina:</span><span class="sxs-lookup"><span data-stu-id="7b280-126">Use hello following command tooupdate your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="7b280-127">Użyj następującego polecenia toodownload hello Node.js plików binarnych tooyour Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-127">Use hello following command toodownload hello Node.js binaries tooyour Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7b280-128">Użyj hello następujące pliki binarne hello tooinstall polecenia:</span><span class="sxs-lookup"><span data-stu-id="7b280-128">Use hello following command tooinstall hello binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="7b280-129">Użyj hello następujące polecenie tooverify Node.js v6.10.2 zostały zainstalowane pomyślnie:</span><span class="sxs-lookup"><span data-stu-id="7b280-129">Use hello following command tooverify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a><span data-ttu-id="7b280-130">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="7b280-130">Clone hello repositories</span></span>

<span data-ttu-id="7b280-131">Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="7b280-131">If you haven't already done so, clone hello required repositories by running hello following commands on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="7b280-132">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="7b280-132">Update hello device connection string</span></span>

<span data-ttu-id="7b280-133">Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-133">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="7b280-134">Znajdź wiersz hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-134">Find hello line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="7b280-135">Zastąp symbole zastępcze hello hello urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="7b280-135">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="7b280-136">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="7b280-136">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="run-hello-sample"></a><span data-ttu-id="7b280-137">Uruchom hello próbki</span><span class="sxs-lookup"><span data-stu-id="7b280-137">Run hello sample</span></span>

<span data-ttu-id="7b280-138">Witaj uruchom następujące polecenia tooinstall hello pakietów wymagań wstępnych dla przykładu hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-138">Run hello following commands tooinstall hello prerequisite packages for hello sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

<span data-ttu-id="7b280-139">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="7b280-139">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="7b280-140">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7b280-140">Enter hello command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

<span data-ttu-id="7b280-141">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="7b280-141">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="7b280-143">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="7b280-143">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="7b280-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b280-144">Next steps</span></span>

<span data-ttu-id="7b280-145">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="7b280-145">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
