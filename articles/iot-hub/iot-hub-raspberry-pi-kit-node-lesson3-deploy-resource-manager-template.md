---
title: "Nawiązać Pi malina (węzeł) Azure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="68b03-104">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="68b03-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="68b03-105">[Środowisko Azure Functions](../azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze.</span><span class="sxs-lookup"><span data-stu-id="68b03-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="68b03-106">Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="68b03-107">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="68b03-107">What you will do</span></span>
<span data-ttu-id="68b03-108">Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="68b03-109">Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="68b03-110">Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="68b03-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="68b03-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="68b03-111">What you will learn</span></span>
<span data-ttu-id="68b03-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="68b03-112">In this article, you will learn:</span></span>

* <span data-ttu-id="68b03-113">Jak używać [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) wdrażania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="68b03-114">Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="68b03-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="68b03-115">What you need</span></span>
<span data-ttu-id="68b03-116">Pomyślnie zakończono:</span><span class="sxs-lookup"><span data-stu-id="68b03-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="68b03-117">Rozpoczynanie pracy z malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="68b03-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="68b03-118">Utworzenie Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="68b03-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="68b03-119">Otwórz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="68b03-119">Open the sample app</span></span>
<span data-ttu-id="68b03-120">Otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="68b03-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struktura repozytorium](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="68b03-122">`app.js` w pliku `app` podfolder jest plik źródłowy klucza.</span><span class="sxs-lookup"><span data-stu-id="68b03-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="68b03-123">Ten plik źródłowy zawiera kod, aby wysłać wiadomość 20 razy do Centrum IoT i blink LED dla każdej wiadomości wysyłane.</span><span class="sxs-lookup"><span data-stu-id="68b03-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="68b03-124">`arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="68b03-125">`arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68b03-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="68b03-126">`ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68b03-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="68b03-127">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="68b03-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="68b03-128">Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="68b03-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametry szablonu usługi Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="68b03-130">Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="68b03-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="68b03-131">Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma.</span><span class="sxs-lookup"><span data-stu-id="68b03-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="68b03-132">Prefiks zapewnia, że nazwa zasobu jest globalnie unikatowy, aby uniknąć konfliktu.</span><span class="sxs-lookup"><span data-stu-id="68b03-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="68b03-133">Nie należy używać dash lub numer początkowej w prefiksie.</span><span class="sxs-lookup"><span data-stu-id="68b03-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="68b03-134">Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="68b03-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="68b03-135">Trwa około pięciu minut utworzyć tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="68b03-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="68b03-136">Podczas tworzenia zasobu jest w toku, możesz przejść do następnego artykułu.</span><span class="sxs-lookup"><span data-stu-id="68b03-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="68b03-137">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="68b03-137">Summary</span></span>
<span data-ttu-id="68b03-138">Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="68b03-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="68b03-139">Można teraz wdrożyć i uruchomić przykładowe wysyłać urządzenia do chmury na Pi.</span><span class="sxs-lookup"><span data-stu-id="68b03-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68b03-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68b03-140">Next steps</span></span>
[<span data-ttu-id="68b03-141">Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury w malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="68b03-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

