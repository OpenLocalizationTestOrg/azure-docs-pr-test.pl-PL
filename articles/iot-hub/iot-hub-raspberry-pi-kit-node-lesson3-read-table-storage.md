---
featureFlags: usabilla
title: "Nawiązać Pi malina (węzeł) Azure IoT — lekcji 3: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości urządzenia do chmury, ponieważ są one zapisywane do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Pobieranie danych z chmury, iot usługi w chmurze"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 9965bd54-61da-479b-aaad-5604850a2be5
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 60084906c05ff9e5396f8e2378d73f7ac939d8df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="e7d71-104">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="e7d71-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="e7d71-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e7d71-105">What you will do</span></span>
<span data-ttu-id="e7d71-106">Monitorowanie komunikatów urządzenia do chmury, które są wysyłane z 3 Pi malina do Centrum IoT, jak komunikaty są zapisywane do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d71-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="e7d71-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e7d71-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e7d71-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e7d71-108">What you will learn</span></span>
<span data-ttu-id="e7d71-109">W tym artykule dowiesz się, jak używać zadań odczytu komunikatu gulp odczytywać komunikaty utrwalone w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d71-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e7d71-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e7d71-110">What you need</span></span>
<span data-ttu-id="e7d71-111">Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom przykładową aplikację Azure migania malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="e7d71-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="e7d71-112">Odczytaj wiadomości z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="e7d71-112">Read new messages from your storage account</span></span>
<span data-ttu-id="e7d71-113">W poprzednim artykule został uruchomiony przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="e7d71-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="e7d71-114">Komunikaty przykładowej aplikacji wysyłane do Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e7d71-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="e7d71-115">Komunikaty wysyłane do Centrum IoT są przechowywane w magazynie tabel Azure przy użyciu aplikacji Azure — funkcja.</span><span class="sxs-lookup"><span data-stu-id="e7d71-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="e7d71-116">Należy parametry połączenia magazynu Azure do czytania wiadomości z magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d71-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="e7d71-117">Aby odczytać wiadomości przechowywanych w magazynie tabel Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e7d71-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="e7d71-118">Pobierz ciąg połączenia, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="e7d71-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="e7d71-119">Pierwsze polecenie pobiera `storage name` używanej w drugiego polecenia można pobrać ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="e7d71-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="e7d71-120">Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="e7d71-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="e7d71-121">Otwórz plik konfiguracji `config-raspberrypi.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e7d71-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="e7d71-122">Zastąp `[Azure storage connection string]` z parametrami połączenia uzyskano w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="e7d71-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="e7d71-123">Zapisz `config-raspberrypi.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="e7d71-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="e7d71-124">Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e7d71-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="e7d71-125">Logika do odczytu z magazynu tabel Azure znajduje się w `azure-table.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="e7d71-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
    ![run--gulp odczytu magazynu](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message.png)

## <a name="summary"></a><span data-ttu-id="e7d71-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e7d71-127">Summary</span></span>
<span data-ttu-id="e7d71-128">Został pomyślnie połączony Pi Centrum IoT w chmurze i używany migania przykładowej aplikacji do wysyłania wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="e7d71-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="e7d71-129">Aplikacji Azure — funkcja jest również używane do przechowywania wiadomości przychodzących Centrum IoT do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d71-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="e7d71-130">Teraz można wysłać wiadomości chmury do urządzenia z Centrum IoT do Pi.</span><span class="sxs-lookup"><span data-stu-id="e7d71-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7d71-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7d71-131">Next steps</span></span>
[<span data-ttu-id="e7d71-132">Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="e7d71-132">Run the sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md)

