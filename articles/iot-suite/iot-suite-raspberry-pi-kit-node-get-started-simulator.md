---
title: "Nawiązać Pi malina pakiet IoT Azure przy użyciu środowiska Node.js w usłudze symulowane telemetrii | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Microsoft Azure IoT Starter Kit malinowe pi 3 i pakiet Azure IoT. Użyj Node.js do nawiązania połączenia zdalnego rozwiązanie monitorowania sieci Pi malina wysłać symulowanych dane telemetryczne do chmury i Odpowiedz na metody wywoływane z poziomu pulpitu nawigacyjnego rozwiązania."
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
ms.openlocfilehash: 43fbfe2f2c5fb86e496c4419f9565365cf89830a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a><span data-ttu-id="1d034-104">Twoje malina Pi 3 nawiązać połączenie zdalne rozwiązanie monitorowania i wysłać symulowanych dane telemetryczne przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d034-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send simulated telemetry using Node.js</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="1d034-105">Ten samouczek pokazuje, jak używać malina Pi 3 do symulowania temperatury i wilgotności dane do wysłania do chmury.</span><span class="sxs-lookup"><span data-stu-id="1d034-105">This tutorial shows you how to use the Raspberry Pi 3 to simulate temperature and humidity data to send to the cloud.</span></span> <span data-ttu-id="1d034-106">W samouczku:</span><span class="sxs-lookup"><span data-stu-id="1d034-106">The tutorial uses:</span></span>

- <span data-ttu-id="1d034-107">Raspbian systemu operacyjnego, język programowania Node.js i Microsoft Azure IoT SDK dla środowiska Node.js do zaimplementowania urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="1d034-107">Raspbian OS, the Node.js programming language, and the Microsoft Azure IoT SDK for Node.js to implement a sample device.</span></span>
- <span data-ttu-id="1d034-108">Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="1d034-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="1d034-109">Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d034-109">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="1d034-110">Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1d034-110">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="1d034-111">Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="1d034-111">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="1d034-112">Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="1d034-112">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="1d034-113">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="1d034-113">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="1d034-114">Pobierz i skonfiguruj próbki</span><span class="sxs-lookup"><span data-stu-id="1d034-114">Download and configure the sample</span></span>

<span data-ttu-id="1d034-115">Można teraz pobrać i konfigurowania zdalnego monitorowania aplikacji klienckiej na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="1d034-115">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="1d034-116">Instalowanie środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="1d034-116">Install Node.js</span></span>

<span data-ttu-id="1d034-117">Jeśli jeszcze tego nie zrobiono tego wcześniej, należy zainstalować Node.js na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="1d034-117">If you haven't done so already, install Node.js on your Raspberry Pi.</span></span> <span data-ttu-id="1d034-118">Zestaw SDK IoT dla środowiska Node.js wymaga wersji 0.11.5 Node.js lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1d034-118">The IoT SDK for Node.js requires version 0.11.5 of Node.js or later.</span></span> <span data-ttu-id="1d034-119">Poniższe kroki pokazują, jak zainstalować Node.js v6.10.2 na Twoje Pi malina:</span><span class="sxs-lookup"><span data-stu-id="1d034-119">The following steps show you how to install Node.js v6.10.2 on your Raspberry Pi:</span></span>

1. <span data-ttu-id="1d034-120">Można zaktualizować Twojego Pi malina, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d034-120">Use the following command to update your Raspberry Pi:</span></span>

    ```sh
    sudo apt-get update
    ```

1. <span data-ttu-id="1d034-121">Podczas pobierania plików binarnych Node.js z Pi malina, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d034-121">Use the following command to download the Node.js binaries to your Raspberry Pi:</span></span>

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="1d034-122">Aby zainstalować pliki binarne, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d034-122">Use the following command to install the binaries:</span></span>

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. <span data-ttu-id="1d034-123">Użyj następującego polecenia, aby sprawdzić, czy pomyślnie zainstalowano Node.js v6.10.2:</span><span class="sxs-lookup"><span data-stu-id="1d034-123">Use the following command to verify you have installed Node.js v6.10.2 successfully:</span></span>

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a><span data-ttu-id="1d034-124">Klonowanie repozytoria</span><span class="sxs-lookup"><span data-stu-id="1d034-124">Clone the repositories</span></span>

<span data-ttu-id="1d034-125">Jeśli jeszcze tego nie zrobiono, klonowanie wymagane repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="1d034-125">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="1d034-126">Zaktualizuj parametry połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="1d034-126">Update the device connection string</span></span>

<span data-ttu-id="1d034-127">Otwieranie przykładowego pliku źródłowego w **nano** edytora za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d034-127">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="1d034-128">Znajdź wiersz:</span><span class="sxs-lookup"><span data-stu-id="1d034-128">Find the line:</span></span>

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

<span data-ttu-id="1d034-129">Zastąp symbole zastępcze urządzenia i Centrum IoT informacji utworzony i zapisany na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d034-129">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="1d034-130">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="1d034-130">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="1d034-131">Uruchom próbki</span><span class="sxs-lookup"><span data-stu-id="1d034-131">Run the sample</span></span>

<span data-ttu-id="1d034-132">Uruchom następujące polecenia, aby zainstalować wstępnie wymagane pakiety przykładowej:</span><span class="sxs-lookup"><span data-stu-id="1d034-132">Run the following commands to install the prerequisite packages for the sample:</span></span>

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

<span data-ttu-id="1d034-133">Teraz możesz uruchomić program przykładowy na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="1d034-133">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="1d034-134">Wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d034-134">Enter the command:</span></span>

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

<span data-ttu-id="1d034-135">Następujące przykładowe dane wyjściowe jest przykład danych wyjściowych, widocznej na Pi malina w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d034-135">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="1d034-137">Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="1d034-137">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="1d034-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d034-138">Next steps</span></span>

<span data-ttu-id="1d034-139">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="1d034-139">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
