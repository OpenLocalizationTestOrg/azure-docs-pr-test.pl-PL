---
title: "Connect Arduino (C) do Azure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do Adafruit piór M0 WiFi, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania danych do chmury"
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
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="148c5-104">Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="148c5-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="148c5-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="148c5-105">What you will do</span></span>
<span data-ttu-id="148c5-106">W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wysyłania komunikatów do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="148c5-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="148c5-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="148c5-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="148c5-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="148c5-108">What you will learn</span></span>
<span data-ttu-id="148c5-109">Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia na tablicy Arduino Arduino przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="148c5-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="148c5-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="148c5-110">What you need</span></span>
* <span data-ttu-id="148c5-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="148c5-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="148c5-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="148c5-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="148c5-113">Ciąg połączenia urządzenia jest używany do nawiązania tablicy Arduino Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="148c5-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="148c5-114">Parametry połączenia Centrum IoT jest używany do nawiązania połączenia tożsamości tego urządzenia, który reprezentuje tablicy Arduino w Centrum IoT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="148c5-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="148c5-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="148c5-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="148c5-116">Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="148c5-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="148c5-117">Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="148c5-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="148c5-118">`{my hub name}`jest to nazwa określonej podczas tworzenia Centrum IoT i zarejestrowana Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="148c5-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="148c5-119">Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="148c5-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="148c5-120">Użyj `mym0wifi` jako wartość `{device id}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="148c5-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="148c5-121">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="148c5-121">Configure the device connection</span></span>
<span data-ttu-id="148c5-122">Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="148c5-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="148c5-123">Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="148c5-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="148c5-124">Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino:</span><span class="sxs-lookup"><span data-stu-id="148c5-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Odnajdywanie urządzeń][device-discovery]

2. <span data-ttu-id="148c5-126">Otwórz plik `config.json` w folderze lekcji i Dodaj wartość znaleziony numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="148c5-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="148c5-128">Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="148c5-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="148c5-129">System macOS lub Ubuntu rozpoczyna się od `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="148c5-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="148c5-130">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="148c5-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="148c5-131">Otwórz plik konfiguracji urządzenia `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="148c5-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![arduino.json konfiguracji][config-arduino-json]

5. <span data-ttu-id="148c5-133">Wprowadź następujące elementy zastępcze w `config-arduino.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="148c5-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="148c5-134">Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który jest połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="148c5-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="148c5-135">Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="148c5-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="148c5-136">Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg.</span><span class="sxs-lookup"><span data-stu-id="148c5-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="148c5-137">Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="148c5-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="148c5-138">Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="148c5-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="148c5-139">Nie ma potrzeby `azure_storage_connection_string` w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="148c5-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="148c5-140">Zachować, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="148c5-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="148c5-141">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="148c5-141">Deploy and run the sample application</span></span>
<span data-ttu-id="148c5-142">Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="148c5-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="148c5-143">Uruchamia zadanie gulp domyślne `install-tools` i `run` zadania po kolei.</span><span class="sxs-lookup"><span data-stu-id="148c5-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="148c5-144">Gdy możesz [wdrożonych aplikacji migania][deployed-the-blink-app], oddzielnie uruchomiono tych zadań.</span><span class="sxs-lookup"><span data-stu-id="148c5-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="148c5-145">Sprawdź, czy działa przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="148c5-145">Verify that the sample application works</span></span>
<span data-ttu-id="148c5-146">Powinien zostać wyświetlony interfejs GPIO #0 lokalnego LED migający przez co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="148c5-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="148c5-147">Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="148c5-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="148c5-148">Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="148c5-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="148c5-149">Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="148c5-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="148c5-151">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="148c5-151">Summary</span></span>
<span data-ttu-id="148c5-152">Został wdrożony i Uruchom nowe migania przykładową aplikację na tablicy Arduino do wysyłania wiadomości urządzenia do chmury do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="148c5-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="148c5-153">Wiadomości jest teraz monitorować, ponieważ są one zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="148c5-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="148c5-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="148c5-154">Next steps</span></span>
<span data-ttu-id="148c5-155">[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="148c5-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md