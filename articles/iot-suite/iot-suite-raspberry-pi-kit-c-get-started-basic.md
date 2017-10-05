---
title: "Pi malina nawiązać połączenie za pomocą C z czujników rzeczywistych pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Microsoft Azure IoT Starter Kit malinowe pi 3 i pakiet Azure IoT. Użyj C do nawiązania połączenia zdalnego rozwiązanie monitorowania sieci Pi malina wysłać dane telemetryczne z czujników w chmurze i Odpowiedz na metody wywoływane z poziomu pulpitu nawigacyjnego rozwiązania."
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
ms.openlocfilehash: 418108e8236518d2671abca0f06f1ae8159d6442
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a><span data-ttu-id="63590-104">Twoje malina Pi 3 nawiązać połączenie zdalne rozwiązanie monitorowania i wysyłania danych telemetrycznych z czujnika rzeczywistych za pomocą C</span><span class="sxs-lookup"><span data-stu-id="63590-104">Connect your Raspberry Pi 3 to the remote monitoring solution and send telemetry from a real sensor using C</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

<span data-ttu-id="63590-105">W tym samouczku przedstawiono sposób Microsoft Azure IoT startowy do malina Pi 3 umożliwia tworzenie czytnik temperatury i wilgotności, który może komunikować się z chmurą.</span><span class="sxs-lookup"><span data-stu-id="63590-105">This tutorial shows you how to use the Microsoft Azure IoT Starter Kit for Raspberry Pi 3 to develop a temperature and humidity reader that can communicate with the cloud.</span></span> <span data-ttu-id="63590-106">W samouczku:</span><span class="sxs-lookup"><span data-stu-id="63590-106">The tutorial uses:</span></span>

- <span data-ttu-id="63590-107">Raspbian systemu operacyjnego, język programowania C i Microsoft Azure IoT SDK dla języka C do zaimplementowania urządzenia próbki.</span><span class="sxs-lookup"><span data-stu-id="63590-107">Raspbian OS, the C programming language, and the Microsoft Azure IoT SDK for C to implement a sample device.</span></span>
- <span data-ttu-id="63590-108">Pakiet IoT zdalne monitorowanie wstępnie skonfigurowane rozwiązanie jako zaplecza opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="63590-108">The IoT Suite remote monitoring preconfigured solution as the cloud-based back end.</span></span>

## <a name="overview"></a><span data-ttu-id="63590-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="63590-109">Overview</span></span>

<span data-ttu-id="63590-110">W tym samouczku zostaną wykonane następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="63590-110">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="63590-111">Wdrożenie wystąpienia programu zdalnego wstępnie skonfigurowane rozwiązanie monitorowania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63590-111">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="63590-112">Ten krok automatycznie wdraża i konfiguruje wiele usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63590-112">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="63590-113">Konfigurowanie czujniki i urządzenia do komunikowania się z komputerem i zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="63590-113">Set up your device and sensors to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="63590-114">Zaktualizuj przykładowy kod urządzenia do nawiązania połączenia zdalnego rozwiązanie monitorowania i wysłać dane telemetryczne, które można wyświetlić na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="63590-114">Update the sample device code to connect to the remote monitoring solution, and send telemetry that you can view on the solution dashboard.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> <span data-ttu-id="63590-115">Zdalne rozwiązanie monitorowania udostępnia zestaw usług platformy Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63590-115">The remote monitoring solution provisions a set of Azure services in your Azure subscription.</span></span> <span data-ttu-id="63590-116">Wdrożenie odzwierciedla architektury przedsiębiorstwa prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="63590-116">The deployment reflects a real enterprise architecture.</span></span> <span data-ttu-id="63590-117">Aby uniknąć niepotrzebnych wykorzystania platformy Azure, opłat, należy usunąć wystąpienia wstępnie skonfigurowanego rozwiązania na azureiotsuite.com po zakończeniu z nim.</span><span class="sxs-lookup"><span data-stu-id="63590-117">To avoid unnecessary Azure consumption charges, delete your instance of the preconfigured solution at azureiotsuite.com when you have finished with it.</span></span> <span data-ttu-id="63590-118">Jeśli potrzebujesz ponownie wstępnie skonfigurowanego rozwiązania, można go łatwo odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="63590-118">If you need the preconfigured solution again, you can easily recreate it.</span></span> <span data-ttu-id="63590-119">Aby uzyskać więcej informacji na temat zmniejszenie zużycia podczas wykonywania zdalnego rozwiązanie monitorowania, zobacz [Konfigurowanie pakiet IoT Azure wstępnie rozwiązań dla celów demonstracyjnych][lnk-demo-config].</span><span class="sxs-lookup"><span data-stu-id="63590-119">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a><span data-ttu-id="63590-120">Pobierz i skonfiguruj próbki</span><span class="sxs-lookup"><span data-stu-id="63590-120">Download and configure the sample</span></span>

<span data-ttu-id="63590-121">Można teraz pobrać i konfigurowania zdalnego monitorowania aplikacji klienckiej na Twoje malina Pi.</span><span class="sxs-lookup"><span data-stu-id="63590-121">You can now download and configure the remote monitoring client application on your Raspberry Pi.</span></span>

### <a name="clone-the-repositories"></a><span data-ttu-id="63590-122">Klonowanie repozytoria</span><span class="sxs-lookup"><span data-stu-id="63590-122">Clone the repositories</span></span>

<span data-ttu-id="63590-123">Jeśli jeszcze tego nie zrobiono, klonowanie wymagane repozytoriów, uruchamiając następujące polecenia w terminalu na Twoje Pi:</span><span class="sxs-lookup"><span data-stu-id="63590-123">If you haven't already done so, clone the required repositories by running the following commands in a terminal on your Pi:</span></span>

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-the-device-connection-string"></a><span data-ttu-id="63590-124">Zaktualizuj parametry połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="63590-124">Update the device connection string</span></span>

<span data-ttu-id="63590-125">Otwieranie przykładowego pliku źródłowego w **nano** edytora za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="63590-125">Open the sample source file in the **nano** editor using the following command:</span></span>

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
```

<span data-ttu-id="63590-126">Znajdź następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="63590-126">Locate the following lines:</span></span>

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

<span data-ttu-id="63590-127">Zastąp symbole zastępcze urządzenia i Centrum IoT informacji utworzony i zapisany na początku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="63590-127">Replace the placeholder values with the device and IoT Hub information you created and saved at the start of this tutorial.</span></span> <span data-ttu-id="63590-128">Zapisz zmiany (**Ctrl-O**, **Enter**) i zamknij Edytor (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="63590-128">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>

## <a name="build-the-sample"></a><span data-ttu-id="63590-129">Tworzyć przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="63590-129">Build the sample</span></span>

<span data-ttu-id="63590-130">Zainstaluj wstępnie wymagane pakiety dla Microsoft Azure IoT urządzenia SDK dla języka C, uruchamiając następujące polecenia w terminalu na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="63590-130">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by running the following commands in a terminal on the Raspberry Pi:</span></span>

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

<span data-ttu-id="63590-131">Można teraz tworzyć zaktualizowane przykładowe rozwiązanie na Pi malina:</span><span class="sxs-lookup"><span data-stu-id="63590-131">You can now build the updated sample solution on the Raspberry Pi:</span></span>

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

<span data-ttu-id="63590-132">Teraz możesz uruchomić program przykładowy na malina Pi.</span><span class="sxs-lookup"><span data-stu-id="63590-132">You can now run the sample program on the Raspberry Pi.</span></span> <span data-ttu-id="63590-133">Wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="63590-133">Enter the command:</span></span>

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

<span data-ttu-id="63590-134">Następujące przykładowe dane wyjściowe jest przykład danych wyjściowych, widocznej na Pi malina w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="63590-134">The following sample output is an example of the output you see at the command prompt on the Raspberry Pi:</span></span>

![Dane wyjściowe z aplikacji malinowe Pi][img-raspberry-output]

<span data-ttu-id="63590-136">Naciśnij klawisz **Ctrl-C** aby zamknąć program w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="63590-136">Press **Ctrl-C** to exit the program at any time.</span></span>

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a><span data-ttu-id="63590-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63590-137">Next steps</span></span>

<span data-ttu-id="63590-138">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="63590-138">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
