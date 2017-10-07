---
title: "Connect Intel Edison (C) tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello przykładowej C aplikacji z usługi GitHub i uruchomić gulp toodeploy tej aplikacji tooyour Intel Edison tablicy. Ta przykładowa aplikacja miga tablicy toohello LED połączone hello co dwie sekundy."
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
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="62500-105">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="62500-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="62500-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="62500-106">What you will do</span></span>
<span data-ttu-id="62500-107">Klonowanie hello przykładowej C aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="62500-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="62500-108">Witaj przykładowej aplikacji miga tablicy toohello LED połączone hello co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="62500-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="62500-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="62500-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="62500-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="62500-110">What you will learn</span></span>
* <span data-ttu-id="62500-111">Jak toodeploy i wykonywania hello przykładowej aplikacji na Edison.</span><span class="sxs-lookup"><span data-stu-id="62500-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="62500-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="62500-112">What you need</span></span>
<span data-ttu-id="62500-113">Użytkownik pomyślnie ukończona hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="62500-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="62500-114">[Skonfiguruj urządzenie][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="62500-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="62500-115">[Pobierz narzędzia hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="62500-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="62500-116">Otwórz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="62500-116">Open hello sample application</span></span>
<span data-ttu-id="62500-117">Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62500-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="62500-118">Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="62500-119">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="62500-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Struktura repozytorium][repo-structure]

<span data-ttu-id="62500-121">Plik Hello w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="62500-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="62500-122">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="62500-122">Install application dependencies</span></span>
<span data-ttu-id="62500-123">Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="62500-124">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="62500-124">Configure hello device connection</span></span>
<span data-ttu-id="62500-125">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62500-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="62500-126">Generowanie pliku konfiguracji urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="62500-127">plik konfiguracji Hello `config-edison.json` zawiera poświadczenia użytkownika hello używasz toolog tooEdison.</span><span class="sxs-lookup"><span data-stu-id="62500-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="62500-128">przeciek hello tooavoid poświadczeń użytkownika hello plik konfiguracji jest generowany w podfolderze hello `.iot-hub-getting-started` hello folderu macierzystego na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="62500-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="62500-129">Otwórz plik konfiguracji urządzenia hello w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="62500-130">Zastąp symbol zastępczy hello `[device hostname or IP address]` i `[device password]` z adresem IP hello i hasło, które są oznaczone w dół w poprzedniej lekcji.</span><span class="sxs-lookup"><span data-stu-id="62500-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="62500-132">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="62500-132">Congratulations!</span></span> <span data-ttu-id="62500-133">Witaj pierwszy przykładowej aplikacji Edison została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="62500-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="62500-134">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="62500-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="62500-135">Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Edison</span><span class="sxs-lookup"><span data-stu-id="62500-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="62500-136">Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Edison, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="62500-137">To zadanie może potrwać długo toocomplete, w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="62500-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="62500-138">Go wymaga toobe uruchomić tylko raz dla jednego Edison.</span><span class="sxs-lookup"><span data-stu-id="62500-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="62500-139">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="62500-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="62500-140">Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62500-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="62500-141">Weryfikowanie działania aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="62500-141">Verify hello app works</span></span>
<span data-ttu-id="62500-142">Witaj przykładowej aplikacji kończy się automatycznie po hello LED miga do 20 razy.</span><span class="sxs-lookup"><span data-stu-id="62500-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="62500-143">Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów] [ troubleshooting] dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="62500-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![Migający LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="62500-145">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="62500-145">Summary</span></span>
<span data-ttu-id="62500-146">Zainstalowaniu hello wymagane narzędzia toowork z Edison i przykładowej aplikacji tooEdison tooblink hello LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="62500-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="62500-147">Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy tooAzure Edison toosend Centrum IoT i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="62500-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62500-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62500-148">Next steps</span></span>
<span data-ttu-id="62500-149">[Pobierz hello Azure narzędzia][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="62500-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
