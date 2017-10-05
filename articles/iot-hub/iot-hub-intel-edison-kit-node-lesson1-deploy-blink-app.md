---
title: "Edison firmy Intel (węzeł) nawiązania połączenia platformy Azure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie aplikacji przykładowej C z serwisu GitHub, a następnie uruchom gulp do wdrożenia tej aplikacji do tablicy Intel Edison. Ta przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino doprowadziły projektów, arduino doprowadziły migania, kod migania arduino doprowadziły, program migania arduino, arduino migania przykład"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8490fbbf14183432c665165412f00955d6323580
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="17198-105">Tworzenie i wdrażanie aplikacji blink</span><span class="sxs-lookup"><span data-stu-id="17198-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="17198-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="17198-106">What you will do</span></span>
<span data-ttu-id="17198-107">Klonowanie aplikacji przykładowej C z usługi GitHub i wdrażanie przykładowej aplikacji do firmy Intel Edison za pomocą narzędzia gulp.</span><span class="sxs-lookup"><span data-stu-id="17198-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="17198-108">Przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="17198-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="17198-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="17198-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="17198-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="17198-110">What you will learn</span></span>
* <span data-ttu-id="17198-111">Jak wdrożyć i uruchomić aplikację przykładową na Edison.</span><span class="sxs-lookup"><span data-stu-id="17198-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="17198-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="17198-112">What you need</span></span>
<span data-ttu-id="17198-113">Pomyślnie zakończono następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="17198-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="17198-114">[Skonfiguruj urządzenie][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="17198-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="17198-115">[Pobierz narzędzia][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="17198-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="17198-116">Otwórz aplikację przykładową</span><span class="sxs-lookup"><span data-stu-id="17198-116">Open the sample application</span></span>
<span data-ttu-id="17198-117">Aby otworzyć aplikację przykładową, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17198-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="17198-118">Klonowanie repozytorium przykładowej z serwisu GitHub, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17198-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="17198-119">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="17198-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

<span data-ttu-id="17198-121">Plik `app` podfolder jest plik źródłowy klucza, który zawiera kod służący do kontroli LED.</span><span class="sxs-lookup"><span data-stu-id="17198-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="17198-122">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="17198-122">Install application dependencies</span></span>
<span data-ttu-id="17198-123">Zainstaluj biblioteki oraz inne moduły potrzebnych dla aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17198-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="17198-124">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="17198-124">Configure the device connection</span></span>
<span data-ttu-id="17198-125">Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17198-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="17198-126">Generowanie pliku konfiguracji urządzenia, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17198-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="17198-127">Plik konfiguracji `config-edison.json` zawiera poświadczenia użytkownika używane do logowania się do Edison.</span><span class="sxs-lookup"><span data-stu-id="17198-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="17198-128">W celu uniknięcia wycieku poświadczeń użytkownika, plik konfiguracji jest generowany w podfolderze `.iot-hub-getting-started` folderu macierzystego na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="17198-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="17198-129">Otwórz plik konfiguracji urządzeń w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17198-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="17198-130">Zastąp symbol zastępczy `[device hostname or IP address]` i `[device password]` przy użyciu adresu IP i hasła, który oznaczony w dół w poprzedniej lekcji.</span><span class="sxs-lookup"><span data-stu-id="17198-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="17198-132">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="17198-132">Congratulations!</span></span> <span data-ttu-id="17198-133">Pierwszy Przykładowa aplikacja dla Edison została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="17198-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="17198-134">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="17198-134">Deploy and run the sample application</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="17198-135">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="17198-135">Deploy and run the sample app</span></span>
<span data-ttu-id="17198-136">Wdrażanie i uruchamianie aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="17198-136">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="17198-137">Weryfikowanie działania aplikacji</span><span class="sxs-lookup"><span data-stu-id="17198-137">Verify the app works</span></span>
<span data-ttu-id="17198-138">Przykładowa aplikacja kończy się automatycznie po LED miga do 20 razy.</span><span class="sxs-lookup"><span data-stu-id="17198-138">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="17198-139">Jeśli nie widzisz migający LED, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="17198-139">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![Migający LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="17198-141">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="17198-141">Summary</span></span>
<span data-ttu-id="17198-142">Zainstalowaniu wymagane narzędzia do pracy z Edison i przykładowej aplikacji do Edison miga LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="17198-142">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="17198-143">Teraz można tworzyć, wdrażać i uruchom inną aplikację przykładową, która łączy Edison Centrum IoT Azure do wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="17198-143">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17198-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17198-144">Next steps</span></span>
<span data-ttu-id="17198-145">[Pobierz narzędzia Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="17198-145">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
