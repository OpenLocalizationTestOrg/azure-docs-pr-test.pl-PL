---
title: "Urządzeń Sensor tag & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połączenia bramy z Centrum IoT i Sensor tag"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie internet rzeczy, iot toolkit
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="88e70-104">Rozpoczynanie pracy z IoT bramy Starter Kit z Sensor tag</span><span class="sxs-lookup"><span data-stu-id="88e70-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="88e70-105">Sensor tag</span><span class="sxs-lookup"><span data-stu-id="88e70-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="88e70-106">Symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="88e70-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="88e70-107">W tym samouczku, rozpoczyna się od podstawy pracy z uczenia [IoT bramy Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="88e70-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="88e70-108">Będzie działać z NUC firmy Intel, z systemem Linux rzeki knie i [Sensor tag analizy czasowej](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="88e70-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="88e70-109">Dowiesz się jak do seamleesly łączyć urządzenia do chmury przy użyciu Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="88e70-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="88e70-110">**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="88e70-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="88e70-111">**Nie masz Sensor tag?:** [zaczynać się symulowane urządzenie](iot-hub-gateway-kit-c-sim-get-started.md) lub [kupić Sensor tag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="88e70-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="88e70-112">Lekcja 1. Konfigurowanie urządzenia NUC</span><span class="sxs-lookup"><span data-stu-id="88e70-112">Lesson 1: Configure your NUC</span></span>
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="88e70-114">W tej lekcji Konfigurowanie NUC firmy Intel (dalej jednostki z przetwarzania danych) w zestawie jako bramy usługi Azure IoT, zainstaluj pakiet Azure IoT Edge na NUC i uruchom przykładową aplikację, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="88e70-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="88e70-115">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="88e70-116">Przejdź do [Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="88e70-117">Lekcja 2. Tworzenie centrum IoT Hub</span><span class="sxs-lookup"><span data-stu-id="88e70-117">Lesson 2: Create your IoT Hub</span></span>
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="88e70-119">W tej lekcji należy zainstalować narzędzia i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="88e70-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="88e70-120">Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="88e70-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="88e70-121">Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.</span><span class="sxs-lookup"><span data-stu-id="88e70-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="88e70-122">Uzyskaj narzędzia</span><span class="sxs-lookup"><span data-stu-id="88e70-122">Get the tools</span></span>
<span data-ttu-id="88e70-123">Zainstaluj narzędzia i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="88e70-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="88e70-124">*Szacowany czas trwania: 20 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="88e70-125">Przejdź do [narzędzia](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="88e70-126">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="88e70-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="88e70-127">Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT i dodać pierwszego urządzenia do Centrum IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88e70-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="88e70-128">*Szacowany czas trwania: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="88e70-129">Przejdź do [tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="88e70-130">Lekcja 3: Odbieranie komunikatów z Sensor tag i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="88e70-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="88e70-131">W tej lekcji użyjesz skryptów do automatyzacji konfiguracji i wykonywania cz przykładową aplikację w Centrum.</span><span class="sxs-lookup"><span data-stu-id="88e70-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="88e70-132">Takie aplikacje używać kolekcji bezpiecznych modułów do agregacji i przekształcania danych, przetwarzanie poleceń lub wykonać dowolną liczbę powiązanych zadań.</span><span class="sxs-lookup"><span data-stu-id="88e70-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="88e70-133">Moduły komunikować się ze sobą za pośrednictwem brokera komunikatów.</span><span class="sxs-lookup"><span data-stu-id="88e70-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="88e70-134">Przykładowa aplikacja ma moduł cz i moduł Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="88e70-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="88e70-135">Moduł cz odbiera dane z cz Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="88e70-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="88e70-136">Moduł Centrum IoT pakietów otrzymanych danych i wysyła go do Centrum IoT przez strukturę bramy w Azure IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="88e70-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="88e70-138">Konfigurowanie i uruchamianie cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="88e70-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="88e70-139">Skonfiguruj połączenie między Sensor tag i bramy.</span><span class="sxs-lookup"><span data-stu-id="88e70-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="88e70-140">Następnie Zakończ konfigurację i uruchom cz przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88e70-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="88e70-141">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="88e70-142">Przejdź do [Konfigurowanie i uruchamianie cz przykładowej aplikacji](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="88e70-143">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="88e70-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="88e70-144">Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="88e70-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="88e70-145">*Szacowany czas trwania: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="88e70-146">Przejdź do [odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="88e70-147">Lekcja 4. Zapisywanie komunikatów w usłudze Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="88e70-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="88e70-148">Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="88e70-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="88e70-150">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="88e70-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="88e70-151">Szablon usługi Azure Resource Manager umożliwia tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="88e70-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="88e70-152">*Szacowany czas trwania: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="88e70-153">Przejdź do [utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="88e70-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="88e70-154">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88e70-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="88e70-155">Monitorowanie wiadomości bramy do chmury, ponieważ są one zapisywane do magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="88e70-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="88e70-156">*Szacowany czas trwania: 5 minut*</span><span class="sxs-lookup"><span data-stu-id="88e70-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="88e70-157">Przejdź do [odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="88e70-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="88e70-158">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="88e70-158">Troubleshooting</span></span>
<span data-ttu-id="88e70-159">Jeśli masz problemy podczas wnioski Szukaj rozwiązań w [Rozwiązywanie problemów](iot-hub-gateway-kit-c-troubleshooting.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="88e70-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="88e70-160">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="88e70-160">Explore more</span></span>
<span data-ttu-id="88e70-161">Odwiedź stronę [strefy developer Kit bramy IoT Intel](http://software.intel.com/iot/microsoft-azure) Aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="88e70-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>