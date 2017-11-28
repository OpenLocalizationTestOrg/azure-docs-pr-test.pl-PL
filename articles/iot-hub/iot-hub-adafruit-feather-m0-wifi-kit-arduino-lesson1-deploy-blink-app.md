---
title: "Połącz Arduino tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello przykładowej Arduino aplikacji z usługi GitHub i uruchomić gulp toodeploy tooyour tej aplikacji Adafruit piór M0 sieci Wi-Fi. Miga, to przykładowa aplikacja hello interfejs GPIO"
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
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="7e27f-105">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="7e27f-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7e27f-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="7e27f-106">What you will do</span></span>
<span data-ttu-id="7e27f-107">Klonowanie hello przykładowej Arduino aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooyour Adafruit piór M0 sieci Wi-Fi Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="7e27f-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="7e27f-108">Witaj przykładowej aplikacji migania Witaj interfejs GPIO #13 na barod PRZEPROWADZONY co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="7e27f-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="7e27f-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="7e27f-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7e27f-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="7e27f-110">What you will learn</span></span>
* <span data-ttu-id="7e27f-111">Jak toodeploy i wykonywania hello przykładowej aplikacji na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="7e27f-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7e27f-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="7e27f-112">What you need</span></span>
<span data-ttu-id="7e27f-113">Użytkownik pomyślnie ukończona hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="7e27f-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="7e27f-114">[Skonfiguruj urządzenie][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="7e27f-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="7e27f-115">[Pobierz narzędzia hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="7e27f-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="7e27f-116">Otwórz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="7e27f-116">Open hello sample application</span></span>
<span data-ttu-id="7e27f-117">Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7e27f-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="7e27f-118">Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7e27f-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="7e27f-119">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="7e27f-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

<span data-ttu-id="7e27f-121">Witaj `app.ino` pliku w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="7e27f-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="7e27f-122">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="7e27f-122">Install application dependencies</span></span>
<span data-ttu-id="7e27f-123">Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7e27f-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="7e27f-124">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="7e27f-124">Configure hello device connection</span></span>
<span data-ttu-id="7e27f-125">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7e27f-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="7e27f-126">Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7e27f-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="7e27f-127">Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino: ![odnajdywania urządzeń][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="7e27f-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="7e27f-128">Witaj Otwórz plik `config.json` w hello lekcji folderu i Dodaj wartości hello hello znaleziono numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="7e27f-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > <span data-ttu-id="7e27f-130">Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="7e27f-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="7e27f-131">System macOS lub Ubuntu rozpoczyna się od `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="7e27f-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="7e27f-132">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="7e27f-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="7e27f-133">Zainstaluj narzędzia hello wymagane dla tablicy Arduino</span><span class="sxs-lookup"><span data-stu-id="7e27f-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="7e27f-134">Zainstaluj hello Azure IoT Hub SDK dla tablicy Arduino, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7e27f-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="7e27f-135">To zadanie może potrwać długo toocomplete, w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7e27f-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="7e27f-136">Zakończ hello uruchomione wystąpienie Arduino IDE, podczas uruchamiania zadania gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="7e27f-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="7e27f-137">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="7e27f-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="7e27f-138">Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7e27f-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="7e27f-139">Weryfikowanie działania aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7e27f-139">Verify hello app works</span></span>
<span data-ttu-id="7e27f-140">Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting-page] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="7e27f-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![Migający LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="7e27f-142">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7e27f-142">Summary</span></span>
<span data-ttu-id="7e27f-143">Zainstalowaniu hello wymagane narzędzia toowork z tablicy Arduino i przykładowej aplikacji tooyour Arduino tablicy tooblink hello LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="7e27f-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="7e27f-144">Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy się z tooAzure tablicy Arduino toosend Centrum IoT i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7e27f-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e27f-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e27f-145">Next steps</span></span>
<span data-ttu-id="7e27f-146">[Pobierz hello Azure narzędzia][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="7e27f-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md