---
title: "Symulowane urządzenie & Azure IoT bramy - 4 lekcji: zapisywanie wiadomości | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Centrum IoT tooyour Intel NUC, zapisanie ich tooAzure tabeli magazynu, a następnie przeczytaj je z chmury hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "przechowywanie danych w chmurze hello, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 230f2708b62b89c6eed2e238efefc1c4da86e373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="0ee66-104">Tworzenie aplikacji funkcji i konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ee66-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="0ee66-105">Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie _funkcje_ (małych fragmentów kodu) w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0ee66-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="0ee66-106">Aplikacja Azure funkcji obsługuje wykonywanie hello funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="0ee66-107">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="0ee66-107">What you will do</span></span>

- <span data-ttu-id="0ee66-108">Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="0ee66-109">Hello Azure funkcji aplikacji nasłuchuje zdarzeń Centrum IoT tooAzure przetwarza przychodzące wiadomości i zapisuje je w magazynie tabel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="0ee66-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0ee66-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="0ee66-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="0ee66-111">What you will learn</span></span>

<span data-ttu-id="0ee66-112">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="0ee66-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0ee66-113">Jak toouse Azure Resource Manager toodeploy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="0ee66-114">Jak toouse Azure funkcji tooprocess aplikacji wiadomości Centrum IoT i zapisanie ich tooa tabeli magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0ee66-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="0ee66-115">What you need</span></span>

<span data-ttu-id="0ee66-116">Możesz pomyślnie ukończona — lekcje poprzedniej hello:</span><span class="sxs-lookup"><span data-stu-id="0ee66-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="0ee66-117">Lekcja 1: Konfigurowanie programu NUC Intel jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="0ee66-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="0ee66-118">Lekcja 2: Przygotowanie komputera hosta i Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="0ee66-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="0ee66-119">Lekcja 3: Otrzymywać wiadomości powitania symulowane urządzenie i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0ee66-119">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="0ee66-120">Otwórz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ee66-120">Open a sample app</span></span>

<span data-ttu-id="0ee66-121">Przejdź tooyour `iot-hub-c-intel-nuc-gateway-getting-started` folderu repozytorium, pliki konfiguracji hello zainicjować i następnie otwórz hello przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0ee66-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struktura repozytorium](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="0ee66-123">Witaj `arm-template.json` pliku jest hello Azure Resource Manager szablon, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="0ee66-124">Witaj `arm-template-param.json` plik jest plikiem konfiguracji hello używane przez hello szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ee66-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="0ee66-125">Witaj `ReceiveDeviceMessages` podfolder zawiera kod Node.js hello hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee66-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="0ee66-126">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0ee66-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="0ee66-127">Aktualizacja hello `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0ee66-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Szablon ARM w formacie json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="0ee66-129">Zastąp `[your IoT Hub name]` z `{my hub name}` określonej Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="0ee66-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="0ee66-130">Po zaktualizowaniu hello `arm-template-param.json` plików, wdrażanie hello tooAzure zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0ee66-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="0ee66-131">Użyj `iot-gateway` jako wartość hello `{resource group name}` nie zmiany wartości hello Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="0ee66-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="0ee66-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="0ee66-132">Summary</span></span>

<span data-ttu-id="0ee66-133">Po utworzeniu sieci tooprocess aplikacji funkcji Azure wiadomości Centrum IoT i toostore konta magazynu Azure, te komunikaty.</span><span class="sxs-lookup"><span data-stu-id="0ee66-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="0ee66-134">Teraz może odczytywać wiadomości, które są wysyłane przez Centrum IoT tooyour bramy.</span><span class="sxs-lookup"><span data-stu-id="0ee66-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ee66-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ee66-135">Next steps</span></span>
<span data-ttu-id="0ee66-136">[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0ee66-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
