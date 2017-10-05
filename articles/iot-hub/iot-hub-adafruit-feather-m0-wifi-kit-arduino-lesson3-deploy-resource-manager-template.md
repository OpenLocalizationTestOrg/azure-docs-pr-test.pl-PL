---
title: "Connect Arduino (C) do Azure IoT — lekcji 3: Wdrażanie szablonu | Dokumentacja firmy Microsoft"
description: "Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Zapisywanie danych w chmurze, dane przechowywane w chmurze, usługi w chmurze iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: be6105927645ae2ec56f6885c61dbcb6faf5b11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="f0965-104">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="f0965-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="f0965-105">[Środowisko Azure Functions](../../articles/azure-functions/functions-overview.md) to rozwiązanie umożliwiające łatwe uruchamianie *funkcje* (małych fragmentów kodu) w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f0965-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="f0965-106">Aplikacja Azure funkcji obsługuje wykonywanie funkcji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="f0965-107">Co spowoduje zrobić</span><span class="sxs-lookup"><span data-stu-id="f0965-107">What will you do</span></span>
<span data-ttu-id="f0965-108">Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f0965-109">Aplikacji Azure — funkcja wykrywa zdarzenia Centrum Azure IoT, przetwarza przychodzące wiadomości i zapisuje je do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="f0965-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony dla tablicy Adafruit piór M0 sieci Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f0965-110">If you have any problems, look for solutions on the [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="f0965-111">Co spowoduje informacje</span><span class="sxs-lookup"><span data-stu-id="f0965-111">What will you learn</span></span>
<span data-ttu-id="f0965-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f0965-112">In this article, you will learn:</span></span>
* <span data-ttu-id="f0965-113">Jak używać [usługi Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) wdrażania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-113">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="f0965-114">Jak używać aplikacji Azure — funkcja przetwarzanie wiadomości Centrum IoT i zapisywania ich w tabeli w magazynie tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="f0965-115">Czego potrzebujesz</span><span class="sxs-lookup"><span data-stu-id="f0965-115">What do you need</span></span>
<span data-ttu-id="f0965-116">Pomyślnie zakończono:</span><span class="sxs-lookup"><span data-stu-id="f0965-116">You must have successfully completed:</span></span>
- <span data-ttu-id="f0965-117">[Rozpoczynanie pracy z tablicy Arduino][get-started]</span><span class="sxs-lookup"><span data-stu-id="f0965-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="f0965-118">[Utworzenie Centrum Azure IoT][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="f0965-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="f0965-119">Otwórz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0965-119">Open the sample app</span></span>
<span data-ttu-id="f0965-120">Otwórz przykładowy projekt w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="f0965-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Struktura repozytorium][repo-structure]

* <span data-ttu-id="f0965-122">`app.ino` w pliku `app` podfolder jest plik źródłowy klucza.</span><span class="sxs-lookup"><span data-stu-id="f0965-122">The `app.ino` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="f0965-123">Ten plik źródłowy zawiera kod, aby wysłać wiadomość 20 razy do Centrum IoT i blink LED dla każdej wiadomości wysyłane.</span><span class="sxs-lookup"><span data-stu-id="f0965-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="f0965-124">`config.json` Zawiera wymagane ustawienia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f0965-124">The `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="f0965-125">`arm-template.json` Plik jest szablonu usługi Azure Resource Manager, który zawiera aplikację funkcji platformy Azure i konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="f0965-126">`arm-template-param.json` Plik jest plikiem konfiguracji używane przez szablon usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0965-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="f0965-127">`ReceiveDeviceMessages` Podfolder zawiera kodu Node.js dla funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0965-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f0965-128">Konfigurowanie szablonów usługi Azure Resource Manager i tworzenie zasobów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f0965-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="f0965-129">Aktualizacja `arm-template-param.json` pliku w Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f0965-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parametry szablonu usługi Azure Resource Manager][arm-template-params]

* <span data-ttu-id="f0965-131">Zastąp **[nazwa Centrum IoT]** z **{mojej nazwy centrum}** określić kiedy należy [tworzenia Centrum IoT i zarejestrowane tablicy Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="f0965-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="f0965-132">Zastąp **[prefiks ciągu dla nowych zasobów]** z dowolnego prefiksu ma.</span><span class="sxs-lookup"><span data-stu-id="f0965-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="f0965-133">Prefiks zapewnia, że nazwa zasobu jest globalnie unikatowy, aby uniknąć konfliktu.</span><span class="sxs-lookup"><span data-stu-id="f0965-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="f0965-134">Nie należy używać dash lub numer początkowej w prefiksie.</span><span class="sxs-lookup"><span data-stu-id="f0965-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="f0965-135">Po zaktualizowaniu `arm-template-param.json` plików, wdrażanie zasobów na platformie Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f0965-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="f0965-136">Trwa około pięciu minut utworzyć tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0965-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="f0965-137">Podczas tworzenia zasobu jest w toku, możesz przejść do następnego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f0965-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="f0965-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f0965-138">Summary</span></span>
<span data-ttu-id="f0965-139">Po utworzeniu aplikacji Azure funkcji do przetwarzania komunikatów Centrum IoT i konto magazynu Azure do przechowywania tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f0965-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="f0965-140">Teraz można wdrożyć i uruchomić przykładowe wysyłać urządzenia do chmury na tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="f0965-140">You can now deploy and run the sample to send device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0965-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0965-141">Next steps</span></span>
<span data-ttu-id="f0965-142">[Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury na tablicy Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="f0965-142">[Run a sample application to send device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md