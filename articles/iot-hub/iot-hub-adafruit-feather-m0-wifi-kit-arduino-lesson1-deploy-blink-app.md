---
title: "Nawiązać Arduino Azure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie przykładowej aplikacji Arduino z serwisu GitHub, a następnie uruchom gulp, aby wdrożyć tę aplikację z Adafruit piór M0 sieci Wi-Fi. Ta przykładowa aplikacja miganie interfejs GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino doprowadziły projektów, arduino doprowadziły migania, kod migania arduino doprowadziły, program migania arduino, arduino migania przykład"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="5e78b-105">Tworzenie i wdrażanie aplikacji blink</span><span class="sxs-lookup"><span data-stu-id="5e78b-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5e78b-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5e78b-106">What you will do</span></span>
<span data-ttu-id="5e78b-107">Klonowanie Arduino przykładowej aplikacji z usługi GitHub i wdrażania przykładowej aplikacji do tablicy Adafruit piór M0 sieci Wi-Fi Arduino za pomocą narzędzia gulp.</span><span class="sxs-lookup"><span data-stu-id="5e78b-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="5e78b-108">Migania aplikacji przykładowy interfejs GPIO #13 na barod PRZEPROWADZONY co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="5e78b-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="5e78b-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="5e78b-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e78b-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5e78b-110">What you will learn</span></span>
* <span data-ttu-id="5e78b-111">Jak wdrożyć i uruchomić aplikację przykładową na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="5e78b-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e78b-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5e78b-112">What you need</span></span>
<span data-ttu-id="5e78b-113">Pomyślnie zakończono następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="5e78b-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="5e78b-114">[Skonfiguruj urządzenie][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="5e78b-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="5e78b-115">[Pobierz narzędzia][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="5e78b-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="5e78b-116">Otwórz aplikację przykładową</span><span class="sxs-lookup"><span data-stu-id="5e78b-116">Open the sample application</span></span>
<span data-ttu-id="5e78b-117">Aby otworzyć aplikację przykładową, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5e78b-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="5e78b-118">Klonowanie repozytorium przykładowej z serwisu GitHub, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5e78b-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="5e78b-119">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="5e78b-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

<span data-ttu-id="5e78b-121">`app.ino` w pliku `app` podfolder jest plik źródłowy klucza, który zawiera kod służący do kontroli LED.</span><span class="sxs-lookup"><span data-stu-id="5e78b-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="5e78b-122">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e78b-122">Install application dependencies</span></span>
<span data-ttu-id="5e78b-123">Zainstaluj biblioteki oraz inne moduły potrzebnych dla aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5e78b-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="5e78b-124">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="5e78b-124">Configure the device connection</span></span>
<span data-ttu-id="5e78b-125">Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5e78b-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="5e78b-126">Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="5e78b-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="5e78b-127">Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino: ![odnajdywania urządzeń][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="5e78b-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="5e78b-128">Otwórz plik `config.json` w folderze lekcji i Dodaj wartość znaleziony numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="5e78b-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="5e78b-130">Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="5e78b-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="5e78b-131">System macOS lub Ubuntu rozpoczyna się od `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="5e78b-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5e78b-132">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e78b-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="5e78b-133">Zainstaluj narzędzia wymagane dla tablicy Arduino</span><span class="sxs-lookup"><span data-stu-id="5e78b-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="5e78b-134">Zainstaluj zestaw SDK Centrum IoT Azure dla tablicy Arduino, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5e78b-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="5e78b-135">To zadanie może zająć dużo czasu, w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5e78b-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="5e78b-136">Zakończ uruchomione wystąpienie Arduino IDE podczas uruchamiania zadania gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="5e78b-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="5e78b-137">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e78b-137">Deploy and run the sample app</span></span>
<span data-ttu-id="5e78b-138">Wdrażanie i uruchamianie aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5e78b-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="5e78b-139">Weryfikowanie działania aplikacji</span><span class="sxs-lookup"><span data-stu-id="5e78b-139">Verify the app works</span></span>
<span data-ttu-id="5e78b-140">Jeśli nie widzisz migający LED, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting-page] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="5e78b-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![Migający LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="5e78b-142">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5e78b-142">Summary</span></span>
<span data-ttu-id="5e78b-143">Zainstalowaniu wymagane narzędzia do pracy z tablicy Arduino i przykładowej aplikacji do tablicy Arduino miga LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="5e78b-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="5e78b-144">Teraz można tworzyć, wdrażać i uruchom inną aplikację przykładową, która łączy tablicy Arduino Centrum IoT Azure do wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="5e78b-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e78b-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e78b-145">Next steps</span></span>
<span data-ttu-id="5e78b-146">[Pobierz narzędzia Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="5e78b-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md