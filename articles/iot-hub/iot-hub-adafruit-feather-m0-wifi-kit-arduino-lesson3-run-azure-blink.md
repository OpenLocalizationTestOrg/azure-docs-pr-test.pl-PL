---
title: "Connect Arduino (C) tooAzure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooAdafruit piór M0 Wi-Fi, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania toocloud danych"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="388fb-104">Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="388fb-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="388fb-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="388fb-105">What you will do</span></span>
<span data-ttu-id="388fb-106">W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na Twojej Adafruit piór M0 sieci Wi-Fi Arduino płycie tego Centrum IoT wysyła komunikaty tooyour.</span><span class="sxs-lookup"><span data-stu-id="388fb-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="388fb-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="388fb-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="388fb-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="388fb-108">What you will learn</span></span>
<span data-ttu-id="388fb-109">Dowiesz się, jak toouse hello system gulp toodeploy narzędzia i uruchomić hello przykładowej aplikacji Arduino na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="388fb-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="388fb-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="388fb-110">What you need</span></span>
* <span data-ttu-id="388fb-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="388fb-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="388fb-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="388fb-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="388fb-113">Witaj ciąg połączenia urządzenia jest używane tooconnect Centrum IoT tooyour Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="388fb-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="388fb-114">Parametry połączenia Centrum IoT Hello są używane tooconnect tożsamości IoT hub toohello urządzenia reprezentujący Arduino Twojego płycie w Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="388fb-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="388fb-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="388fb-116">Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="388fb-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="388fb-117">Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="388fb-118">`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="388fb-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="388fb-119">Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="388fb-120">Użyj `mym0wifi` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="388fb-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="388fb-121">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="388fb-121">Configure hello device connection</span></span>
<span data-ttu-id="388fb-122">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="388fb-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="388fb-123">Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="388fb-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="388fb-124">Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino:</span><span class="sxs-lookup"><span data-stu-id="388fb-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Odnajdywanie urządzeń][device-discovery]

2. <span data-ttu-id="388fb-126">Witaj Otwórz plik `config.json` w hello lekcji folderu i Dodaj wartości hello hello znaleziono numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="388fb-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="388fb-128">Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="388fb-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="388fb-129">System macOS lub Ubuntu rozpoczyna się od `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="388fb-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="388fb-130">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="388fb-131">Plik konfiguracji urządzenia Otwórz hello `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![arduino.json konfiguracji][config-arduino-json]

5. <span data-ttu-id="388fb-133">Wprowadź następujące elementy zastępcze w hello hello `config-arduino.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="388fb-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="388fb-134">Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który połączony toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="388fb-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="388fb-135">Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="388fb-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="388fb-136">Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="388fb-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="388fb-137">Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="388fb-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="388fb-138">Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="388fb-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="388fb-139">Nie ma potrzeby `azure_storage_connection_string` w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="388fb-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="388fb-140">Zachować, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="388fb-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="388fb-141">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="388fb-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="388fb-142">Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="388fb-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="388fb-143">Witaj domyślne gulp zadanie jest uruchamiane `install-tools` i `run` zadania po kolei.</span><span class="sxs-lookup"><span data-stu-id="388fb-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="388fb-144">Gdy możesz [wdrożonych aplikacji migania hello][deployed-the-blink-app], oddzielnie uruchomiono tych zadań.</span><span class="sxs-lookup"><span data-stu-id="388fb-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="388fb-145">Sprawdź, czy działa hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="388fb-145">Verify that hello sample application works</span></span>
<span data-ttu-id="388fb-146">Powinna zostać wyświetlona hello interfejs GPIO #0 lokalnego LED migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="388fb-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="388fb-147">Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="388fb-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="388fb-148">Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="388fb-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="388fb-149">Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="388fb-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="388fb-151">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="388fb-151">Summary</span></span>
<span data-ttu-id="388fb-152">Zostały wdrożone i uruchom hello nowe migania przykładowej aplikacji w Centrum IoT tooyour Arduino tablicy toosend wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="388fb-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="388fb-153">Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="388fb-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="388fb-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="388fb-154">Next steps</span></span>
<span data-ttu-id="388fb-155">[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="388fb-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md