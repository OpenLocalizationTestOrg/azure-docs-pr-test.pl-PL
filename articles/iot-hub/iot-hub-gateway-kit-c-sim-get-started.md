---
title: "Symulowane urządzenie & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połączenia bramy z Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie internet rzeczy, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="0e1e2-104">Rozpoczynanie pracy z IoT bramy Starter Kit z symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="0e1e2-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e1e2-105">Sensor tag</span><span class="sxs-lookup"><span data-stu-id="0e1e2-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="0e1e2-106">Symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="0e1e2-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="0e1e2-107">W tym samouczku, rozpoczyna się od podstawy pracy z uczenia [IoT bramy Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0e1e2-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="0e1e2-108">Będzie działać z NUC firmy Intel, z systemem Linux rzeki knie.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="0e1e2-109">Dowiesz się jak do seamleesly łączyć urządzenia do chmury przy użyciu Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="0e1e2-110">**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0e1e2-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="0e1e2-111">Lekcja 1. Konfigurowanie urządzenia NUC</span><span class="sxs-lookup"><span data-stu-id="0e1e2-111">Lesson 1: Configure your NUC</span></span>
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="0e1e2-113">W tej lekcji Konfigurowanie NUC firmy Intel (dalej jednostki z przetwarzania danych) w zestawie jako bramy usługi Azure IoT, zainstaluj pakiet Azure IoT Edge na NUC i uruchom przykładową aplikację, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="0e1e2-114">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0e1e2-115">Przejdź do [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="0e1e2-116">Lekcja 2. Tworzenie centrum IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0e1e2-116">Lesson 2: Create your IoT Hub</span></span>
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="0e1e2-118">W tej lekcji należy zainstalować narzędzia i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="0e1e2-119">Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="0e1e2-120">Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="0e1e2-121">Uzyskaj narzędzia</span><span class="sxs-lookup"><span data-stu-id="0e1e2-121">Get the tools</span></span>
<span data-ttu-id="0e1e2-122">Zainstaluj narzędzia i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="0e1e2-123">*Szacowany czas trwania: 20 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="0e1e2-124">Przejdź do [narzędzia](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="0e1e2-125">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="0e1e2-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="0e1e2-126">Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT i dodać pierwszego urządzenia do Centrum IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="0e1e2-127">*Szacowany czas trwania: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="0e1e2-128">Przejdź do [tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="0e1e2-129">Lekcja 3: Odbieranie komunikatów z symulowane urządzenie i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0e1e2-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="0e1e2-130">W tej lekcji użyjesz skryptów do automatyzacji konfiguracji i wykonywania aplikacji symulowane urządzenie w Centrum.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="0e1e2-131">Aplikacja symulowane urządzenie generuje przykładowych danych temperatury i wysyła go do modułu Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="0e1e2-132">Moduł Centrum IoT pakietów otrzymanych danych i wysyła go do Centrum IoT przez strukturę bramy w Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="0e1e2-134">Konfigurowanie i uruchamianie symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="0e1e2-134">Configure and run a simulated device</span></span>
<span data-ttu-id="0e1e2-135">Przygotuj przykładowych kodów.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-135">Prepare the sample codes.</span></span> <span data-ttu-id="0e1e2-136">Następnie skonfiguruj i uruchom przykładową aplikację symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="0e1e2-137">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0e1e2-138">Przejdź do [Konfigurowanie i uruchamianie symulowane urządzenie](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="0e1e2-139">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0e1e2-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="0e1e2-140">Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="0e1e2-141">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="0e1e2-142">Przejdź do [odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="0e1e2-143">Lekcja 4. Zapisywanie komunikatów w usłudze Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="0e1e2-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="0e1e2-144">Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="0e1e2-146">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="0e1e2-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="0e1e2-147">Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="0e1e2-148">*Szacowany czas trwania: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="0e1e2-149">Przejdź do [utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="0e1e2-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="0e1e2-150">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e1e2-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="0e1e2-151">Monitorowanie wiadomości bramy do chmury, ponieważ są one zapisywane do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="0e1e2-152">*Szacowany czas trwania: 5 minut*</span><span class="sxs-lookup"><span data-stu-id="0e1e2-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="0e1e2-153">Przejdź do [odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0e1e2-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0e1e2-154">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="0e1e2-154">Troubleshooting</span></span>
<span data-ttu-id="0e1e2-155">Jeśli masz problemy podczas wnioski Szukaj rozwiązań w [Rozwiązywanie problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="0e1e2-156">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="0e1e2-156">Explore more</span></span>
<span data-ttu-id="0e1e2-157">Odwiedź stronę [strefy developer Kit bramy IoT Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) Aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="0e1e2-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>