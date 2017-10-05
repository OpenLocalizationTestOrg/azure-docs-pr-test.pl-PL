---
title: "Urządzeń Sensor tag & bramy IoT Azure - lekcja 4: Tabela magazynów | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Intel NUC do Centrum IoT, zapisanie ich do magazynu tabel Azure, a następnie przeczytaj je z chmury."
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
ms.openlocfilehash: 72659ef3a7fd2f6011590d37176fd05503269aff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="d347e-104">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d347e-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="d347e-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="d347e-105">What you will do</span></span>

- <span data-ttu-id="d347e-106">Uruchom przykładową aplikację bramy dla bramy wysyłania komunikatów do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d347e-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="d347e-107">Następnie uruchom przykładowy kod na komputerze hosta odczytywać wiadomości z magazynem tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-107">Then run a sample code on your host computer to read the messages in your Azure Table storage.</span></span> 

<span data-ttu-id="d347e-108">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d347e-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d347e-109">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d347e-109">What you will learn</span></span>

<span data-ttu-id="d347e-110">Jak używać narzędzia gulp uruchamiać kod przykładowy można odczytywać wiadomości w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d347e-111">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="d347e-111">What you need</span></span>

<span data-ttu-id="d347e-112">Został pomyślnie wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d347e-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="d347e-113">[Utworzone konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d347e-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="d347e-114">[Uruchom przykładową aplikację bramy](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span><span class="sxs-lookup"><span data-stu-id="d347e-114">[Run the gateway sample application](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md).</span></span>
- <span data-ttu-id="d347e-115">[Odbieranie wiadomości w Centrum IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="d347e-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="d347e-116">Pobrać parametry połączenia magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d347e-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="d347e-117">Na początku tej lekcji pomyślnie utworzono konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="d347e-118">Można pobrać ciągu połączenia z kontem magazynu platformy Azure, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d347e-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="d347e-119">Lista wszystkich kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="d347e-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="d347e-120">Pobierz ciąg połączenia usługi azure storage.</span><span class="sxs-lookup"><span data-stu-id="d347e-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="d347e-121">Użyj bramy iot jako wartość `{resource group name}` nie zmiany wartości Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="d347e-121">Use iot-gateway as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="d347e-122">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="d347e-122">Configure the device connection</span></span>

<span data-ttu-id="d347e-123">Aktualizacja `config-azure.json` plików, dzięki czemu przykładowy kod, który jest uruchamiany na komputerze hosta może odczytywać wiadomości w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="d347e-124">Aby skonfigurować połączenie z urządzeniem, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d347e-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="d347e-125">Otwórz plik konfiguracji urządzenia `config-azure.json` , uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d347e-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![konfiguracja](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="d347e-127">Zastąp `[Azure storage connection string]` przy użyciu parametrów połączenia magazynu Azure uzyskany.</span><span class="sxs-lookup"><span data-stu-id="d347e-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="d347e-128">`[IoT hub connection string]`już powinna zostać zastąpiona w sekcji [odczytywać wiadomości z Centrum IoT Azure](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) w Lesson3.</span><span class="sxs-lookup"><span data-stu-id="d347e-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="d347e-129">Odczytywać wiadomości w magazynie tabel Azure</span><span class="sxs-lookup"><span data-stu-id="d347e-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="d347e-130">Uruchom przykładową aplikację bramy i odbieranie wiadomości magazynu tabel Azure za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d347e-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="d347e-131">Centrum IoT wyzwala aplikacji funkcji platformy Azure do zapisywania wiadomości do magazynu tabel Azure po odebraniu nowego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="d347e-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="d347e-132">`gulp run` Polecenie uruchamia aplikację przykładową bramy, która wysyła komunikaty do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d347e-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="d347e-133">Z `table-storage` parametru, jego również spowoduje utworzenie proces podrzędny komunikat zapisane w magazynie tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="d347e-134">Komunikaty, które są wysyłane i odebranych są wszystkie natychmiast wyświetlane na tym samym oknie konsoli w komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="d347e-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="d347e-135">Wystąpienie aplikacji przykładowej zakończy się automatycznie w 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="d347e-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![Odczyt gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table.png)


## <a name="summary"></a><span data-ttu-id="d347e-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d347e-137">Summary</span></span>

<span data-ttu-id="d347e-138">Uruchomiono przykładowy kod umożliwiający odczytywać wiadomości z magazynem tabel Azure zapisane przez aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d347e-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>