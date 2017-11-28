---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT — lekcji 3: monitorowanie wiadomości | Dokumentacja firmy Microsoft"
description: "Monitorowanie wiadomości powitania od urządzenia do chmury, ponieważ są one zapisywane tooyour magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
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
ms.openlocfilehash: 8f6371482123bc9aa12db55b38d3e8863645f981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="1f736-104">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="1f736-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1f736-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="1f736-105">What you will do</span></span>
<span data-ttu-id="1f736-106">Monitor hello urządzenia do chmury wiadomości, które są wysyłane z Centrum IoT tooyour Intel Edison jako wiadomości powitania są zapisywane tooyour magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1f736-106">Monitor hello device-to-cloud messages that are sent from Intel Edison tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="1f736-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1f736-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1f736-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="1f736-108">What you will learn</span></span>
<span data-ttu-id="1f736-109">W tym artykule dowiesz się, jak toouse wiadomości tooread zadanie odczytu wiadomości powitania od gulp utrwalone w magazynem tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1f736-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1f736-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="1f736-110">What you need</span></span>
<span data-ttu-id="1f736-111">Przed rozpoczęciem tego procesu, musi pomyślnie ukończył [Uruchom hello Azure migania przykładowej aplikacji na Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="1f736-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="1f736-112">Odczytaj wiadomości z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="1f736-112">Read new messages from your storage account</span></span>
<span data-ttu-id="1f736-113">W poprzednim artykule hello na Edison uruchomiono przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f736-113">In hello previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="1f736-114">aplikacja przykładowa Hello wysyłane Centrum Azure IoT tooyour wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1f736-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="1f736-115">Centrum IoT tooyour wysłane wiadomości powitania są przechowywane do magazynu tabel Azure za pomocą hello Azure funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f736-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="1f736-116">Należy hello magazynu Azure połączenia ciąg tooread wiadomości z magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1f736-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="1f736-117">tooread wiadomości przechowywanych w swoim magazynem tabel Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f736-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="1f736-118">Pobierz ciąg połączenia hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="1f736-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="1f736-119">Witaj pierwsze polecenie pobiera hello `storage name` używanej w hello drugiego polecenia tooget hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="1f736-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="1f736-120">Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="1f736-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="1f736-121">Plik konfiguracji Otwórz hello `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1f736-121">Open hello configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="1f736-122">Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia hello uzyskano w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="1f736-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="1f736-123">Zapisz hello `config-edison.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="1f736-123">Save hello `config-edison.json` file.</span></span>
5. <span data-ttu-id="1f736-124">Ponowne wysłanie wiadomości i je odczytać z magazynu tabel Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1f736-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="1f736-125">Witaj logiki odczytu z magazynu tabel Azure znajduje się w hello `azure-table.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="1f736-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>

   ![run--gulp odczytu magazynu][gulp run]

## <a name="summary"></a><span data-ttu-id="1f736-127">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1f736-127">Summary</span></span>
<span data-ttu-id="1f736-128">Pomyślnie zostały połączone z Centrum IoT tooyour Edison w chmurze hello i używane wiadomości powitania od migania przykładowej aplikacji toosend urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="1f736-128">You've successfully connected Edison tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="1f736-129">Możesz również hello Azure funkcji aplikacji toostore przychodzące IoT Centrum wiadomości tooyour magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="1f736-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="1f736-130">Teraz można wysłać wiadomości chmury do urządzenia z Twojej tooEdison Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1f736-130">You can now send cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f736-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f736-131">Next steps</span></span>
<span data-ttu-id="1f736-132">[Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="1f736-132">[Run a sample application tooreceive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md