---
title: "Connect Intel Edison (C) do Azure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie aplikacji przykładowej C z serwisu GitHub, a następnie uruchom gulp do wdrożenia tej aplikacji do tablicy Intel Edison. Ta przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino doprowadziły projektów, arduino doprowadziły migania, kod migania arduino doprowadziły, program migania arduino, arduino migania przykład"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="6f83b-105">Tworzenie i wdrażanie aplikacji blink</span><span class="sxs-lookup"><span data-stu-id="6f83b-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="6f83b-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="6f83b-106">What you will do</span></span>
<span data-ttu-id="6f83b-107">Klonowanie aplikacji przykładowej C z usługi GitHub i wdrażanie przykładowej aplikacji do firmy Intel Edison za pomocą narzędzia gulp.</span><span class="sxs-lookup"><span data-stu-id="6f83b-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="6f83b-108">Przykładowa aplikacja miga LED podłączone do tablicy co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="6f83b-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="6f83b-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="6f83b-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="6f83b-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="6f83b-110">What you will learn</span></span>
* <span data-ttu-id="6f83b-111">Jak wdrożyć i uruchomić aplikację przykładową na Edison.</span><span class="sxs-lookup"><span data-stu-id="6f83b-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6f83b-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="6f83b-112">What you need</span></span>
<span data-ttu-id="6f83b-113">Pomyślnie zakończono następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="6f83b-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="6f83b-114">[Skonfiguruj urządzenie][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="6f83b-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="6f83b-115">[Pobierz narzędzia][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="6f83b-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="6f83b-116">Otwórz aplikację przykładową</span><span class="sxs-lookup"><span data-stu-id="6f83b-116">Open the sample application</span></span>
<span data-ttu-id="6f83b-117">Aby otworzyć aplikację przykładową, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6f83b-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="6f83b-118">Klonowanie repozytorium przykładowej z serwisu GitHub, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="6f83b-119">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f83b-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

<span data-ttu-id="6f83b-121">Plik `app` podfolder jest plik źródłowy klucza, który zawiera kod służący do kontroli LED.</span><span class="sxs-lookup"><span data-stu-id="6f83b-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="6f83b-122">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f83b-122">Install application dependencies</span></span>
<span data-ttu-id="6f83b-123">Zainstaluj biblioteki oraz inne moduły potrzebnych dla aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="6f83b-124">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="6f83b-124">Configure the device connection</span></span>
<span data-ttu-id="6f83b-125">Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6f83b-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="6f83b-126">Generowanie pliku konfiguracji urządzenia, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="6f83b-127">Plik konfiguracji `config-edison.json` zawiera poświadczenia użytkownika używane do logowania się do Edison.</span><span class="sxs-lookup"><span data-stu-id="6f83b-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="6f83b-128">W celu uniknięcia wycieku poświadczeń użytkownika, plik konfiguracji jest generowany w podfolderze `.iot-hub-getting-started` folderu macierzystego na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6f83b-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="6f83b-129">Otwórz plik konfiguracji urządzeń w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="6f83b-130">Zastąp symbol zastępczy `[device hostname or IP address]` i `[device password]` przy użyciu adresu IP i hasła, który oznaczony w dół w poprzedniej lekcji.</span><span class="sxs-lookup"><span data-stu-id="6f83b-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="6f83b-132">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="6f83b-132">Congratulations!</span></span> <span data-ttu-id="6f83b-133">Pierwszy Przykładowa aplikacja dla Edison została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="6f83b-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="6f83b-134">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f83b-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="6f83b-135">Zainstaluj Centrum IoT Azure SDK na Edison</span><span class="sxs-lookup"><span data-stu-id="6f83b-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="6f83b-136">Zainstaluj zestaw SDK usługi Azure IoT Hub na Edison, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="6f83b-137">To zadanie może zająć dużo czasu, w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6f83b-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="6f83b-138">Należy uruchomić tylko raz dla jednego Edison.</span><span class="sxs-lookup"><span data-stu-id="6f83b-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="6f83b-139">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f83b-139">Deploy and run the sample app</span></span>
<span data-ttu-id="6f83b-140">Wdrażanie i uruchamianie aplikacji przykładowej, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f83b-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="6f83b-141">Weryfikowanie działania aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f83b-141">Verify the app works</span></span>
<span data-ttu-id="6f83b-142">Przykładowa aplikacja kończy się automatycznie po LED miga do 20 razy.</span><span class="sxs-lookup"><span data-stu-id="6f83b-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="6f83b-143">Jeśli nie widzisz migający LED, zobacz [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="6f83b-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![Migający LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="6f83b-145">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6f83b-145">Summary</span></span>
<span data-ttu-id="6f83b-146">Zainstalowaniu wymagane narzędzia do pracy z Edison i przykładowej aplikacji do Edison miga LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6f83b-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="6f83b-147">Teraz można tworzyć, wdrażać i uruchom inną aplikację przykładową, która łączy Edison Centrum IoT Azure do wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6f83b-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f83b-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f83b-148">Next steps</span></span>
<span data-ttu-id="6f83b-149">[Pobierz narzędzia Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="6f83b-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
