---
title: "aaaConnect tooAzure Pi malina pakiet IoT z rzeczywistą czujników za pomocą C | Dokumentacja firmy Microsoft"
description: "Użyj hello Microsoft Azure IoT Starter Kit dla hello malina Pi 3 i pakiet IoT Azure. Użyj C tooconnect Twojego toohello Pi malina zdalne monitorowanie rozwiązania, wysyłania danych telemetrycznych z czujników chmury toohello i odpowiadać toomethods wywoływane z pulpitu nawigacyjnego rozwiązania hello."
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="63326-104">Połącz z toohello malina Pi 3 zdalne monitorowanie rozwiązania i wysyłania danych telemetrycznych z czujnika rzeczywistych za pomocą C</span><span class="sxs-lookup"><span data-stu-id="63326-104">Connect your Raspberry Pi 3 toohello remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="63326-105">Ten samouczek pokazuje, jak toouse hello Microsoft Azure IoT Starter Kit dla toodevelop malina Pi 3 czytnik temperatury i wilgotności, który może komunikować się z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="63326-105">This tutorial shows you how toouse hello Microsoft Azure IoT Starter Kit for Raspberry Pi 3 toodevelop a temperature and humidity reader that can communicate with hello cloud.</span></span> <span data-ttu-id="63326-106">samouczku Hello:</span><span class="sxs-lookup"><span data-stu-id="63326-106">hello tutorial uses:</span></span>

- <span data-ttu-id="63326-107">Raspbian systemu operacyjnego, język programowania hello C i hello zestawu SDK usługi Microsoft Azure IoT dla C tooimplement urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="63326-107">Raspbian OS, hello C programming language, and hello Microsoft Azure IoT SDK for C tooimplement a sample device.</span></span>
- <span data-ttu-id="63326-108">monitorowania zdalnego pakiet IoT Hello wstępnie skonfigurowane rozwiązanie jako hello oparte na chmurze zaplecza.</span><span class="sxs-lookup"><span data-stu-id="63326-108">hello IoT Suite remote monitoring preconfigured solution as hello cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="63326-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="63326-109">Overview</span></span>

<span data-ttu-id="63326-110">W tym samouczku można wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="63326-110">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="63326-111">Wdróż wystąpienie wstępnie skonfigurowane rozwiązanie tooyour subskrypcji platformy Azure hello zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="63326-111">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="63326-112">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63326-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="63326-113">Konfigurowanie sieci toocommunicate czujników i urządzeń do komputera i hello zdalne monitorowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="63326-113">Set up your device and sensors toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="63326-114">Zaktualizuj hello próbki urządzenia kod tooconnect toohello zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="63326-114">Update hello sample device code tooconnect toohello remote monitoring solution, and send telemetry that you can view on hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="63326-115">Witaj zdalnego monitorowania przepisów rozwiązania zbiór usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63326-115">hello remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="63326-116">wdrożenie Hello odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="63326-116">hello deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="63326-117">tooavoid opłat niepotrzebnych wykorzystania platformy Azure, usunąć wystąpienie usługi hello wstępnie skonfigurowane rozwiązanie azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="63326-117">tooavoid unnecessary Azure consumption charges, delete your instance of hello preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="63326-118">Jeśli należy ponownie hello wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="63326-118">If you need hello preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="63326-119">Aby uzyskać więcej informacji o zmniejszenie zużycia podczas hello zdalne monitorowanie uruchamia rozwiązania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="63326-119">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a><span data-ttu-id="63326-120">Pobierz i skonfiguruj hello próbki</span><span class="sxs-lookup"><span data-stu-id="63326-120">Download and configure hello sample</span></span>

<span data-ttu-id="63326-121">Można teraz pobrać i skonfigurować aplikację klienta monitorowania zdalnego hello na Twoje Pi malina.</span><span class="sxs-lookup"><span data-stu-id="63326-121">You can now download and configure hello remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-hello-repositories"></a><span data-ttu-id="63326-122">Repozytoria hello w klonowania</span><span class="sxs-lookup"><span data-stu-id="63326-122">Clone hello repositories</span></span>

<span data-ttu-id="63326-123">Jeśli jeszcze tego nie zrobiono, hello w klonowania wymagane hello repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="63326-123">If you haven't already done so, clone hello required repositories by running hello following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a><span data-ttu-id="63326-124">Zaktualizuj parametry połączenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="63326-124">Update hello device connection string</span></span>

<span data-ttu-id="63326-125">Otwórz hello pliku źródłowego próbki w hello **nano** edytora za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="63326-125">Open hello sample source file in hello **nano** editor using hello following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="63326-126">Znajdź hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="63326-126">Locate hello following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="63326-127">Zastąp symbole zastępcze hello hello urządzenia i Centrum IoT informacji utworzony i zapisany pod hello na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="63326-127">Replace hello placeholder values with hello device and IoT Hub information you created and saved at hello start of this tutorial.</span></span> <span data-ttu-id="63326-128">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="63326-128">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>

## <a name="build-hello-sample"></a><span data-ttu-id="63326-129">Przykład Witaj kompilacji</span><span class="sxs-lookup"><span data-stu-id="63326-129">Build hello sample</span></span>

<span data-ttu-id="63326-130">Instalowanie wymagań wstępnych pakietów hello hello zestawu SDK usługi Microsoft Azure IoT urządzenia dla języka C, uruchamiając następujące polecenia w terminalu na powitania Pi malina hello:</span><span class="sxs-lookup"><span data-stu-id="63326-130">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C by running hello following commands in a terminal on hello Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="63326-131">Teraz można tworzyć hello zaktualizowane przykładowe rozwiązanie na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="63326-131">You can now build hello updated sample solution on hello Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="63326-132">Teraz możesz uruchomić program przykładowy hello na powitania malina Pi.</span><span class="sxs-lookup"><span data-stu-id="63326-132">You can now run hello sample program on hello Raspberry Pi.</span></span> <span data-ttu-id="63326-133">Wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="63326-133">Enter hello command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="63326-134">Witaj następujące przykładowe dane wyjściowe jest przykład danych wyjściowych hello, dostępne w wierszu polecenia hello na powitania Pi malina:</span><span class="sxs-lookup"><span data-stu-id="63326-134">hello following sample output is an example of hello output you see at hello command prompt on hello Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="63326-136">Naciśnij klawisz **Ctrl-C** tooexit hello program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="63326-136">Press **Ctrl-C** tooexit hello program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="63326-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63326-137">Next steps</span></span>

<span data-ttu-id="63326-138">Odwiedź hello [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="63326-138">Visit hello [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
