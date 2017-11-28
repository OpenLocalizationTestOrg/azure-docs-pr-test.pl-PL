---
title: "Symulowane urządzenie & Azure IoT bramy - 4 lekcji: zapisywanie wiadomości | Dokumentacja firmy Microsoft"
description: "Zapisywanie wiadomości z Intel NUC do Centrum IoT, zapisanie ich do magazynu tabel Azure, a następnie przeczytaj je z chmury."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
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
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="4ae65-104">Tworzenie aplikacji funkcji i konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4ae65-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="4ae65-105">Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie _funkcje_ (małych fragmentów kodu) w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4ae65-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="4ae65-106">Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="4ae65-107">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="4ae65-107">What you will do</span></span>

- <span data-ttu-id="4ae65-108">Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="4ae65-109">Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="4ae65-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4ae65-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="4ae65-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="4ae65-111">What you will learn</span></span>

<span data-ttu-id="4ae65-112">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="4ae65-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4ae65-113">Jak używać usługi Azure Resource Manager do wdrażania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="4ae65-114">Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4ae65-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="4ae65-115">What you need</span></span>

<span data-ttu-id="4ae65-116">Użytkownik pomyślnie ukończona poprzedniej — lekcje:</span><span class="sxs-lookup"><span data-stu-id="4ae65-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="4ae65-117">Lekcja 1: Konfigurowanie programu NUC Intel jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="4ae65-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="4ae65-118">Lekcja 2: Przygotowanie komputera hosta i Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="4ae65-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="4ae65-119">Lekcja 3: Odbieranie komunikatów z symulowane urządzenie i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="4ae65-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="4ae65-120">Otwórz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ae65-120">Open a sample app</span></span>

<span data-ttu-id="4ae65-121">Przejdź do Twojej `iot-hub-c-intel-nuc-gateway-getting-started` folderu repozytorium zainicjować pliki konfiguracji, a następnie otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4ae65-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![Struktura repozytorium](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="4ae65-123">`arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="4ae65-124">`arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ae65-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="4ae65-125">`ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ae65-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="4ae65-126">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4ae65-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="4ae65-127">Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4ae65-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Szablon ARM w formacie json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="4ae65-129">Zastąp `[your IoT Hub name]` z `{my hub name}` określonej Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="4ae65-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="4ae65-130">Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4ae65-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="4ae65-131">Użyj `iot-gateway` jako wartość `{resource group name}` nie zmiany wartości Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="4ae65-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="4ae65-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4ae65-132">Summary</span></span>

<span data-ttu-id="4ae65-133">Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4ae65-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="4ae65-134">Teraz może odczytywać wiadomości, które są wysyłane przez bramę do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4ae65-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae65-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ae65-135">Next steps</span></span>
<span data-ttu-id="4ae65-136">[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4ae65-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
