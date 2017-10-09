---
title: "Connect Arduino (C) tooAzure IoT — lekcji 3: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości powitania od urządzenia do chmury, ponieważ są one zapisywane tooyour magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9fef18bc9e780e78d95f0c643a5f193125130a5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a6284-104">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="a6284-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a6284-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="a6284-105">What you will do</span></span>
<span data-ttu-id="a6284-106">Monitor hello urządzenia do chmury wiadomości, które są wysyłane z Centrum IoT tooyour tablicy Adafruit piór M0 sieci Wi-Fi Arduino jako wiadomości powitania są zapisywane tooyour magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a6284-106">Monitor hello device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span>

<span data-ttu-id="a6284-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a6284-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a6284-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="a6284-108">What you will learn</span></span>
<span data-ttu-id="a6284-109">W tym artykule dowiesz się, jak toouse wiadomości tooread zadanie odczytu wiadomości powitania od gulp utrwalone w magazynem tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a6284-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a6284-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="a6284-110">What you need</span></span>
<span data-ttu-id="a6284-111">Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom hello Azure migania przykładowej aplikacji na tablicy Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="a6284-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a6284-112">Odczytaj wiadomości z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="a6284-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a6284-113">W poprzednim artykule hello na tablicy Arduino uruchomiono przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6284-113">In hello previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="a6284-114">aplikacja przykładowa Hello wysyłane Centrum Azure IoT tooyour wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a6284-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="a6284-115">Centrum IoT tooyour wysłane wiadomości powitania są przechowywane do magazynu tabel Azure za pomocą hello Azure funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6284-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="a6284-116">Należy hello magazynu Azure połączenia ciąg tooread wiadomości z magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a6284-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="a6284-117">tooread wiadomości przechowywanych w swoim magazynem tabel Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a6284-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a6284-118">Pobierz ciąg połączenia hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a6284-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a6284-119">Witaj pierwsze polecenie pobiera hello `storage name` używanej w hello drugiego polecenia tooget hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="a6284-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="a6284-120">Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="a6284-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="a6284-121">Plik konfiguracji Otwórz hello `config-arduino.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="a6284-121">Open hello configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="a6284-122">Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia hello uzyskano w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="a6284-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="a6284-123">Zapisz hello `config-arduino.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="a6284-123">Save hello `config-arduino.json` file.</span></span>
5. <span data-ttu-id="a6284-124">Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="a6284-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor hello serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="a6284-125">Witaj logiki odczytu z magazynu tabel Azure znajduje się w hello `azure-table.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="a6284-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![run--gulp odczytu magazynu][gulp-run]

## <a name="summary"></a><span data-ttu-id="a6284-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a6284-127">Summary</span></span>
<span data-ttu-id="a6284-128">Pomyślnie zostały połączone z Centrum IoT tooyour Arduino tablicy w chmurze hello i używane wiadomości powitania od migania przykładowej aplikacji toosend urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="a6284-128">You've successfully connected your Arduino board tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="a6284-129">Możesz również hello Azure funkcji aplikacji toostore przychodzące IoT Centrum wiadomości tooyour magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a6284-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="a6284-130">Teraz można wysłać wiadomości chmury do urządzenia z Twojej tooyour Centrum IoT Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="a6284-130">You can now send cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6284-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6284-131">Next steps</span></span>
<span data-ttu-id="a6284-132">[Wysyłanie komunikatów chmury do urządzenia][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="a6284-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md