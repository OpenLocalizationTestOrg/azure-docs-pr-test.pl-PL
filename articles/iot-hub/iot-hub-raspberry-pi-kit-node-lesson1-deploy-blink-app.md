---
featureFlags: usabilla
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Klonowanie hello aplikacji Node.js próbki z serwisu GitHub, a system gulp toodeploy tej tablicy tooyour malina Pi 3 aplikacji. Ta przykładowa aplikacja miga tablicy toohello LED połączone hello co dwie sekundy."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "pi malinowe doprowadziły migania, migania doprowadziły z malinowe pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: a5a03a57-fe86-416f-90ff-6eca17775842
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9732df3009b8342d4872fe2318a975a6251e772b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="cc2f5-105">Tworzenie i wdrażanie aplikacji migania hello</span><span class="sxs-lookup"><span data-stu-id="cc2f5-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cc2f5-106">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="cc2f5-106">What you will do</span></span>
<span data-ttu-id="cc2f5-107">Klonowanie hello aplikacji Node.js próbki z usługi GitHub i użyj hello gulp narzędzie toodeploy hello przykładowej aplikacji tooyour malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-107">Clone hello sample Node.js application from GitHub and use hello gulp tool toodeploy hello sample application tooyour Raspberry Pi 3.</span></span> <span data-ttu-id="cc2f5-108">Witaj przykładowej aplikacji miga tablicy toohello LED połączone hello co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="cc2f5-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cc2f5-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cc2f5-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="cc2f5-110">What you will learn</span></span>
<span data-ttu-id="cc2f5-111">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-111">In this article, you will learn:</span></span>

* <span data-ttu-id="cc2f5-112">Jak toouse hello `device-discover-cli` tooretrieve narzędzie sieci informacji na temat Pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="cc2f5-113">Jak toodeploy i wykonywania hello przykładowej aplikacji na Pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="cc2f5-114">Jak toodeploy i debugowania aplikacji uruchamiany zdalnie na Pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cc2f5-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="cc2f5-115">What you need</span></span>
<span data-ttu-id="cc2f5-116">Użytkownik pomyślnie ukończona hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="cc2f5-117">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="cc2f5-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md)
* [<span data-ttu-id="cc2f5-118">Pobierz narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="cc2f5-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="cc2f5-119">Uzyskaj hello adresu IP i hosta nazwy pi</span><span class="sxs-lookup"><span data-stu-id="cc2f5-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="cc2f5-120">Otwórz wiersz polecenia w systemie Windows lub terminal macOS lub Ubuntu, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="cc2f5-121">Powinny pojawić się dane wyjściowe podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-121">You should see an output that is similar toohello following:</span></span>

![Odnajdywanie urządzeń](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="cc2f5-123">Zwróć uwagę na powitania `IP address` i `hostname` pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="cc2f5-124">Należy w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="cc2f5-125">Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="cc2f5-126">Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="cc2f5-127">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc2f5-127">Clone hello sample application</span></span>
<span data-ttu-id="cc2f5-128">Witaj tooopen przykładowy kod, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-128">tooopen hello sample code, follow these steps:</span></span>

1. <span data-ttu-id="cc2f5-129">Klonuj repozytorium przykładowej hello z serwisu GitHub, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started.git
   ```
2. <span data-ttu-id="cc2f5-130">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
   ```bash
   cd iot-hub-node-raspberrypi-getting-started
   cd Lesson1
   code .
   ```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-mac.png)

<span data-ttu-id="cc2f5-132">Witaj `app.js` pliku w hello `app` podfolder to plik klucza źródła hello, który zawiera hello kodu toocontrol hello LED.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-132">hello `app.js` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="cc2f5-133">Zainstaluj zależności aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc2f5-133">Install application dependencies</span></span>
<span data-ttu-id="cc2f5-134">Zainstaluj hello bibliotek i inne moduły potrzebnych dla aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="cc2f5-135">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="cc2f5-135">Configure hello device connection</span></span>
<span data-ttu-id="cc2f5-136">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="cc2f5-137">Generowanie pliku konfiguracji urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="cc2f5-138">plik konfiguracji Hello `config-raspberrypi.json` zawiera poświadczenia użytkownika hello używasz toolog tooPi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="cc2f5-139">przeciek hello tooavoid poświadczeń użytkownika hello plik konfiguracji jest generowany w podfolderze hello `.iot-hub-getting-started` hello folderu macierzystego na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="cc2f5-140">Otwórz plik konfiguracji urządzenia hello w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
3. <span data-ttu-id="cc2f5-141">Zastąp symbol zastępczy hello `[device hostname or IP address]` hello adres IP lub nazwa hosta hello uzyskano wcześniej w "Uzyskaj hello adresu IP i hosta nazwy pi."</span><span class="sxs-lookup"><span data-stu-id="cc2f5-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="cc2f5-143">Klucz SSH można użyć zamiast nazwy użytkownika i hasła podczas łączenia tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="cc2f5-144">W celu toodo to będzie miał użyciu klucza hello toogenerate **ssh-keygen** i **pi ssh kopiowania id @\<adres urządzenia\>**.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="cc2f5-145">W systemie Windows te polecenia są dostępne w **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="cc2f5-146">Na MacOS należy toorun **brew zainstalować ssh kopiowania id**.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="cc2f5-147">Po pomyślnym przekazaniu klucza toohello hello Pi malina, Zastąp **device_password** z **device_key_path** właściwości w **config raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="cc2f5-148">Wiersze zaktualizowane powinien wyglądać jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="cc2f5-149">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="cc2f5-149">Congratulations!</span></span> <span data-ttu-id="cc2f5-150">Pomyślnie utworzono hello pierwszy przykładowej aplikacji Pi.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="cc2f5-151">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc2f5-151">Deploy and run hello sample application</span></span>
### <a name="install-nodejs-and-npm-on-pi"></a><span data-ttu-id="cc2f5-152">Instalowanie środowiska Node.js i NPM na Pi</span><span class="sxs-lookup"><span data-stu-id="cc2f5-152">Install Node.js and NPM on Pi</span></span>
<span data-ttu-id="cc2f5-153">Zainstaluj środowisko Node.js i NPM na Pi, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-153">Install Node.js and NPM on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="cc2f5-154">To zadanie może potrwać 10 minut toocomplete hello zostanie uruchomiony po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-154">This task might take 10 minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="cc2f5-155">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc2f5-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="cc2f5-156">Wdrażanie i uruchamianie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="cc2f5-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="cc2f5-157">Weryfikowanie działania aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="cc2f5-157">Verify hello app works</span></span>
<span data-ttu-id="cc2f5-158">Powinna zostać wyświetlona hello LED na Pi migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-158">You should now see hello LED on Pi blinking every two seconds.</span></span>  <span data-ttu-id="cc2f5-159">Jeśli nie widzisz migający hello LED, zobacz hello [przewodnik rozwiązywania problemów](iot-hub-raspberry-pi-kit-node-troubleshooting.md) dla rozwiązania toocommon problemów.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="cc2f5-160">![Migający LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="cc2f5-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="cc2f5-161">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="cc2f5-161">Summary</span></span>
<span data-ttu-id="cc2f5-162">Zainstalowaniu hello wymagane narzędzia toowork z Pi i przykładowej aplikacji tooPi tooblink hello LED wdrożone.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="cc2f5-163">Można teraz tworzenie, wdrażanie i uruchom inną aplikację przykładową, która łączy Pi tooAzure toosend Centrum IoT i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="cc2f5-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc2f5-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc2f5-164">Next steps</span></span>
[<span data-ttu-id="cc2f5-165">Pobierz hello Azure narzędzia</span><span class="sxs-lookup"><span data-stu-id="cc2f5-165">Get hello Azure tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)

