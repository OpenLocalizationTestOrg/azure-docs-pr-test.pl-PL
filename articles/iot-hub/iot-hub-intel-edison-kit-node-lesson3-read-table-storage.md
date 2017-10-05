---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — lekcji 3: monitorowanie wiadomości | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości urządzenia do chmury, ponieważ są one zapisywane do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c1a59227cd2bf9d2c9bcaa4212dd5127a95e2779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="a7109-104">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="a7109-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="a7109-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="a7109-105">What you will do</span></span>
<span data-ttu-id="a7109-106">Monitorowanie komunikatów urządzenia do chmury, które są wysyłane z Intel Edison do Centrum IoT, jak komunikaty są zapisywane do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a7109-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="a7109-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="a7109-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7109-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="a7109-108">What you will learn</span></span>
<span data-ttu-id="a7109-109">W tym artykule dowiesz się, jak używać zadań odczytu komunikatu gulp odczytywać komunikaty utrwalone w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a7109-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7109-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="a7109-110">What you need</span></span>
<span data-ttu-id="a7109-111">Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom przykładową aplikację Azure migania na Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="a7109-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="a7109-112">Odczytaj wiadomości z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="a7109-112">Read new messages from your storage account</span></span>
<span data-ttu-id="a7109-113">W poprzednim artykule uruchomiono na Edison przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7109-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="a7109-114">Komunikaty przykładowej aplikacji wysyłane do Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="a7109-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="a7109-115">Komunikaty wysyłane do Centrum IoT są przechowywane w magazynie tabel Azure przy użyciu aplikacji Azure — funkcja.</span><span class="sxs-lookup"><span data-stu-id="a7109-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="a7109-116">Należy parametry połączenia magazynu Azure do czytania wiadomości z magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a7109-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="a7109-117">Aby odczytać wiadomości przechowywanych w magazynie tabel Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a7109-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="a7109-118">Pobierz ciąg połączenia, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7109-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="a7109-119">Pierwsze polecenie pobiera `storage name` używanej w drugiego polecenia można pobrać ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="a7109-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="a7109-120">Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="a7109-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="a7109-121">Otwórz plik konfiguracji `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a7109-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="a7109-122">Zastąp `[Azure storage connection string]` z parametrami połączenia uzyskano w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="a7109-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="a7109-123">Zapisz `config-edison.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="a7109-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="a7109-124">Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a7109-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="a7109-125">Logika do odczytu z magazynu tabel Azure znajduje się w `azure-table.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="a7109-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![run--gulp odczytu magazynu][gulp run]

## <a name="summary"></a><span data-ttu-id="a7109-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a7109-127">Summary</span></span>
<span data-ttu-id="a7109-128">Został pomyślnie połączony Edison Centrum IoT w chmurze i używany migania przykładowej aplikacji do wysyłania wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="a7109-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="a7109-129">Aplikacji Azure — funkcja jest również używane do przechowywania wiadomości przychodzących Centrum IoT do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="a7109-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="a7109-130">Teraz można wysłać wiadomości chmury do urządzenia z Centrum IoT na Edison.</span><span class="sxs-lookup"><span data-stu-id="a7109-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7109-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7109-131">Next steps</span></span>
<span data-ttu-id="a7109-132">[Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="a7109-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md