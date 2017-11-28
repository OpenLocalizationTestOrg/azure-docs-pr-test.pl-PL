---
title: "Urządzeń Sensor tag & bramy IoT Azure - lekcja 4: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Centrum IoT tooyour Intel NUC, zapisanie ich tooAzure tabeli magazynu, a następnie przeczytaj je z chmury hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Pobieranie danych z chmury, iot usługi w chmurze"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 8ca78045-ad92-4a6a-90f1-05f9668e6f0e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29525b084eb4d6e6dfcb16d9b34f78f075d30b7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="3858d-104">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3858d-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3858d-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="3858d-105">What you will do</span></span>

- <span data-ttu-id="3858d-106">Uruchom hello bramy przykładowej aplikacji na bramie wysyłanej wiadomości tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3858d-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="3858d-107">Następnie uruchom przykładowy kod w wiadomości powitania tooread komputera hosta w magazynem tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-107">Then run a sample code on your host computer tooread hello messages in your Azure Table storage.</span></span> 

<span data-ttu-id="3858d-108">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3858d-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3858d-109">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="3858d-109">What you will learn</span></span>

<span data-ttu-id="3858d-110">Jak toouse hello system gulp narzędzie toorun przykładowy kod tooread wiadomości powitania w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3858d-111">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="3858d-111">What you need</span></span>

<span data-ttu-id="3858d-112">Został pomyślnie hello następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="3858d-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="3858d-113">[Utworzony hello Azure funkcji aplikacji i konto magazynu Azure hello](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="3858d-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="3858d-114">[Uruchom hello bramy przykładowej aplikacji](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="3858d-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="3858d-115">[Odbieranie wiadomości w Centrum IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="3858d-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="3858d-116">Pobrać parametry połączenia magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="3858d-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="3858d-117">Na początku tej lekcji pomyślnie utworzono konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="3858d-118">tooget hello parametry połączenia z kontem magazynu platformy Azure hello, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3858d-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="3858d-119">Lista wszystkich kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="3858d-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="3858d-120">Pobierz ciąg połączenia usługi azure storage.</span><span class="sxs-lookup"><span data-stu-id="3858d-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="3858d-121">Użyj bramy iot jako wartość hello `{resource group name}` nie zmiany wartości hello Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="3858d-121">Use iot-gateway as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="3858d-122">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="3858d-122">Configure hello device connection</span></span>

<span data-ttu-id="3858d-123">Aktualizacja hello `config-azure.json` plików, dzięki czemu hello przykładowy kod, który jest uruchamiany na komputerze hosta hello może odczytywać wiadomości w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="3858d-124">tooconfigure hello połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3858d-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="3858d-125">Plik konfiguracji urządzenia Otwórz hello `config-azure.json` , uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3858d-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![konfiguracja](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="3858d-127">Zastąp `[Azure storage connection string]` z hello parametry połączenia magazynu Azure uzyskany.</span><span class="sxs-lookup"><span data-stu-id="3858d-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="3858d-128">`[IoT hub connection string]`już powinna zostać zastąpiona w sekcji [odczytywać wiadomości z Centrum IoT Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) w Lesson3.</span><span class="sxs-lookup"><span data-stu-id="3858d-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="3858d-129">Odczytywać wiadomości w magazynie tabel Azure</span><span class="sxs-lookup"><span data-stu-id="3858d-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="3858d-130">Uruchom hello bramy przykładowej aplikacji i odbieranie wiadomości magazynu tabel Azure przez hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3858d-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="3858d-131">Centrum IoT wyzwala wiadomości toosave aplikacji funkcji platformy Azure do magazynu tabel Azure po odebraniu nowego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3858d-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="3858d-132">Witaj `gulp run` polecenie uruchamia aplikację przykładową bramy, która wysyła Centrum IoT tooyour wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3858d-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="3858d-133">Z `table-storage` parametru, jego również spowoduje utworzenie hello tooreceive procesu podrzędnego zapisać komunikatu w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="3858d-134">wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="3858d-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="3858d-135">wystąpienie aplikacji przykładowej Hello zakończy się automatycznie w 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="3858d-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Odczyt gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="3858d-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3858d-137">Summary</span></span>

<span data-ttu-id="3858d-138">Uruchomiono wiadomości powitania tooread hello przykładowy kod w magazynie tabel Azure zapisane przez aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3858d-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
