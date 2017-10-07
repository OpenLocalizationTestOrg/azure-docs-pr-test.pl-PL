---
title: "aaaConnect tooAzure Pi malina pakiet IoT za pomocą C z symulowanego telemetrii | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysłać symulowanych telemetrii toohello chmury i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a><span data-ttu-id="ddc26-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysłać symulowanych dane telemetryczne za pomocą C</span><span class="sxs-lookup"><span data-stu-id="ddc26-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send simulated telemetry using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="ddc26-105">Ten samouczek pokazuje, jak hello toouse malina Pi 3 toosimulate temperatury i wilgotności danych toosend toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="ddc26-105">This tutorial shows you how toouse hello Raspberry Pi 3 toosimulate temperature and humidity data toosend toohello cloud.</span></span> <span data-ttu-id="ddc26-106">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="ddc26-106">hello tutorial uses:</span></span>

- <span data-ttu-id="ddc26-107">Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="ddc26-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="ddc26-108">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="ddc26-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="ddc26-109">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc26-109">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="ddc26-110">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ddc26-110">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="ddc26-111">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="ddc26-111">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="ddc26-112">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="ddc26-112">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="ddc26-113">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="ddc26-113">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="ddc26-114">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="ddc26-114">Download and configure hello sample</span></span>

<span data-ttu-id="ddc26-115">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="ddc26-115">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="ddc26-116">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="ddc26-116">Clone hello repositories</span></span>

<span data-ttu-id="ddc26-117">Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="ddc26-117">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="ddc26-118">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="ddc26-118">Update hello device connection string</span></span>

<span data-ttu-id="ddc26-119">Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ddc26-119">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="ddc26-120">Znajdź hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="ddc26-120">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="ddc26-121">Zastąp symbole zastępcze hello hello urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ddc26-121">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="ddc26-122">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="ddc26-122">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="ddc26-123">Przykład Witaj kompilacji</span><span class="sxs-lookup"><span data-stu-id="ddc26-123">Build hello sample</span></span>

<span data-ttu-id="ddc26-124">Instalowanie wymagań wstępnych pakietów hello hello zestawu SDK usługi Microsoft Azure IoT urządzenia dla języka C, uruchamiając następujące polecenia w terminalu na powitania Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="ddc26-124">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="ddc26-125">Teraz można tworzyć hello zaktualizowane przykładowe rozwiązanie na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="ddc26-125">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

<span data-ttu-id="ddc26-126">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="ddc26-126">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="ddc26-127">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ddc26-127">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="ddc26-128">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="ddc26-128">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="ddc26-130">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="ddc26-130">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a><span data-ttu-id="ddc26-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ddc26-131">Next steps</span></span>

<span data-ttu-id="ddc26-132">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="ddc26-132">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
