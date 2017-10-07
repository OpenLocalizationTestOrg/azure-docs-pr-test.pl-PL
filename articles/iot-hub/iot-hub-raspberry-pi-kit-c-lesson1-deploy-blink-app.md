---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello aplikacji przykładowej C z serwisu GitHub, a system gulp toodeploy tej tablicy tooyour malina Pi 3 aplikacji. Ta przykładowa aplikacja miga tablicy toohello LED połączone hello co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi malinowe doprowadziły migania, migania doprowadziły z malinowe pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="4ad35-105">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="4ad35-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4ad35-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="4ad35-106">What you will do</span></span>
<span data-ttu-id="4ad35-107">Klonowanie hello przykładowej C aplikacji z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooRaspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="4ad35-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="4ad35-108">Witaj przykładowej aplikacji miga tablicy toohello LED połączone hello co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="4ad35-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="4ad35-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4ad35-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4ad35-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="4ad35-110">What you will learn</span></span>
<span data-ttu-id="4ad35-111">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="4ad35-111">In this article, you will learn:</span></span>

* <span data-ttu-id="4ad35-112">Jak toouse hello `device-discover-cli` tooretrieve narzędzie sieci informacji na temat Pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="4ad35-113">Jak toodeploy i wykonywania hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="4ad35-114">Jak toodeploy i debugowania aplikacji uruchamiany zdalnie na Pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ad35-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="4ad35-115">What you need</span></span>
<span data-ttu-id="4ad35-116">Użytkownik pomyślnie ukończona hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="4ad35-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="4ad35-117">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="4ad35-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="4ad35-118">Pobierz narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="4ad35-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="4ad35-119">Uzyskaj hello adresu IP i hosta nazwy pi</span><span class="sxs-lookup"><span data-stu-id="4ad35-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="4ad35-120">Otwórz wiersz polecenia w systemie Windows lub terminal macOS lub Ubuntu, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="4ad35-121">Powinny pojawić się dane wyjściowe podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ad35-121">You should see an output that is similar toohello following:</span></span>

![Odnajdywanie urządzeń](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="4ad35-123">Zwróć uwagę na powitania `IP address` i `hostname` pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="4ad35-124">Należy w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4ad35-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad35-125">Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="4ad35-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="4ad35-126">Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4ad35-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="4ad35-127">Otwórz hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ad35-127">Open hello sample application</span></span>
<span data-ttu-id="4ad35-128">Witaj tooopen przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4ad35-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="4ad35-129">Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="4ad35-130">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="4ad35-132">Witaj `main.c` pliku w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="4ad35-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="4ad35-133">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ad35-133">Install application dependencies</span></span>
<span data-ttu-id="4ad35-134">Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="4ad35-135">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="4ad35-135">Configure hello device connection</span></span>
<span data-ttu-id="4ad35-136">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4ad35-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="4ad35-137">Generowanie pliku konfiguracji urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="4ad35-138">plik konfiguracji Hello `config-raspberrypi.json` zawiera poświadczenia użytkownika hello używasz toolog tooPi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="4ad35-139">przeciek hello tooavoid poświadczeń użytkownika hello plik konfiguracji jest generowany w podfolderze hello `.iot-hub-getting-started` hello folderu macierzystego na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4ad35-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="4ad35-140">Otwórz plik konfiguracji urządzenia hello w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="4ad35-141">Zastąp symbol zastępczy hello `[device hostname or IP address]` hello adres IP lub nazwa hosta hello uzyskano wcześniej w "Uzyskaj hello adresu IP i hosta nazwy pi."</span><span class="sxs-lookup"><span data-stu-id="4ad35-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="4ad35-143">Klucz SSH można użyć zamiast nazwy użytkownika i hasła podczas łączenia tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="4ad35-144">W celu toodo to będzie miał użyciu klucza hello toogenerate **ssh-keygen** i **pi ssh kopiowania id @\<adres urządzenia\>**.</span><span class="sxs-lookup"><span data-stu-id="4ad35-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="4ad35-145">W systemie Windows te polecenia są dostępne w **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="4ad35-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="4ad35-146">Na MacOS należy toorun **brew zainstalować ssh kopiowania id**.</span><span class="sxs-lookup"><span data-stu-id="4ad35-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="4ad35-147">Po pomyślnym przekazaniu klucza toohello hello Pi malina, Zastąp **device_password** z **device_key_path** właściwości w **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="4ad35-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="4ad35-148">Wiersze zaktualizowane powinien wyglądać jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="4ad35-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="4ad35-149">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="4ad35-149">Congratulations!</span></span> <span data-ttu-id="4ad35-150">Pomyślnie utworzono hello pierwszy przykładowej aplikacji Pi.</span><span class="sxs-lookup"><span data-stu-id="4ad35-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="4ad35-151">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ad35-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="4ad35-152">Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Pi</span><span class="sxs-lookup"><span data-stu-id="4ad35-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="4ad35-153">Zainstaluj zestaw SDK usługi Azure IoT Hub hello na Pi, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="4ad35-154">To zadanie może potrwać kilka minut toocomplete hello zostanie uruchomiony po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="4ad35-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="4ad35-155">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ad35-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="4ad35-156">Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4ad35-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="4ad35-157">Weryfikowanie działania aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="4ad35-157">Verify hello app works</span></span>
<span data-ttu-id="4ad35-158">Witaj przykładowej aplikacji kończy się automatycznie po hello LED miga do 20 razy.</span><span class="sxs-lookup"><span data-stu-id="4ad35-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="4ad35-159">Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-c-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="4ad35-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="4ad35-160">![Migający LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="4ad35-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="4ad35-161">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4ad35-161">Summary</span></span>
<span data-ttu-id="4ad35-162">Zainstalowaniu hello wymagane narzędzia toowork z Pi i przykładowej aplikacji tooPi tooblink hello LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="4ad35-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="4ad35-163">Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy Pi tooAzure toosend Centrum IoT i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4ad35-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ad35-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ad35-164">Next steps</span></span>
[<span data-ttu-id="4ad35-165">Pobierz narzędzia Azure</span><span class="sxs-lookup"><span data-stu-id="4ad35-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

