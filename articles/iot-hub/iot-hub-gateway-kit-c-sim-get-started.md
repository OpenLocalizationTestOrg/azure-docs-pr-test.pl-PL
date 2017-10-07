---
title: "Symulowane urządzenie & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połącz Centrum IoT toohello bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie hello internet rzeczy, iot toolkit
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="2bf7d-104">Rozpoczynanie pracy z IoT bramy Starter Kit z symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="2bf7d-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bf7d-105">Sensor tag</span><span class="sxs-lookup"><span data-stu-id="2bf7d-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="2bf7d-106">Symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="2bf7d-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="2bf7d-107">W tym samouczku, rozpoczyna się od uczenia hello podstawowe informacje dotyczące pracy z [IoT bramy Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="2bf7d-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="2bf7d-108">Będzie działać z NUC firmy Intel, z systemem Linux rzeki knie.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="2bf7d-109">Dowiesz się, jak połączyć tooseamleesly chmury toohello urządzeń przy użyciu Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="2bf7d-110">**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="2bf7d-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="2bf7d-111">Lekcja 1. Konfigurowanie urządzenia NUC</span><span class="sxs-lookup"><span data-stu-id="2bf7d-111">Lesson 1: Configure your NUC</span></span>
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="2bf7d-113">W tej lekcji w hello zestawu jako bramy usługi Azure IoT ustawiona NUC firmy Intel (dalej jednostki z przetwarzania danych), zainstaluj pakiet Azure IoT krawędzi hello na NUC i uruchom funkcję bramy hello tooverify przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="2bf7d-114">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="2bf7d-115">Przejdź do zbyt[Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="2bf7d-116">Lekcja 2. Tworzenie centrum IoT Hub</span><span class="sxs-lookup"><span data-stu-id="2bf7d-116">Lesson 2: Create your IoT Hub</span></span>
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="2bf7d-118">W tej lekcji należy zainstalować narzędzia hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="2bf7d-119">Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="2bf7d-120">Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="2bf7d-121">Pobierz narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="2bf7d-121">Get hello tools</span></span>
<span data-ttu-id="2bf7d-122">Zainstaluj narzędzia hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="2bf7d-123">*Szacowany czas toocomplete: 20 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="2bf7d-124">Przejdź do zbyt[hello narzędzia](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="2bf7d-125">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="2bf7d-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="2bf7d-126">Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT, a następnie dodaj Centrum IoT pierwszy toohello urządzenia przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="2bf7d-127">*Szacowany czas toocomplete: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="2bf7d-128">Przejdź do zbyt[tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="2bf7d-129">Lekcja 3: Otrzymywać wiadomości powitania symulowane urządzenie i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="2bf7d-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="2bf7d-130">W tej lekcji użyjesz konfiguracji hello tooautomate skrypty i wykonywanie aplikacji symulowane urządzenie w Centrum.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="2bf7d-131">Aplikacja symulowane urządzenie Hello generuje przykładowych danych temperatury i wysyła je z modułu Centrum IoT tooan.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="2bf7d-132">Witaj pakietów hello danych odebranych i wysyła je Centrum IoT tooyour za pośrednictwem hello bramy struktura dostępna w programie Azure IoT Edge modułu Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="2bf7d-134">Konfigurowanie i uruchamianie symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="2bf7d-134">Configure and run a simulated device</span></span>
<span data-ttu-id="2bf7d-135">Przygotuj hello przykładowych kodów.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-135">Prepare hello sample codes.</span></span> <span data-ttu-id="2bf7d-136">Następnie skonfiguruj i uruchom hello symulowane urządzenie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="2bf7d-137">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="2bf7d-138">Przejdź do zbyt[Konfigurowanie i uruchamianie symulowane urządzenie](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="2bf7d-139">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="2bf7d-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="2bf7d-140">Uruchom przykładowy kod w wiadomości powitania tooread komputera hosta z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="2bf7d-141">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="2bf7d-142">Przejdź do zbyt[odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="2bf7d-143">Lekcja 4: Zapisywanie wiadomości tooAzure magazynu tabel</span><span class="sxs-lookup"><span data-stu-id="2bf7d-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="2bf7d-144">Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je w magazynie tabel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2bf7d-146">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="2bf7d-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="2bf7d-147">Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="2bf7d-148">*Szacowany czas toocomplete: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="2bf7d-149">Przejdź do zbyt[utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="2bf7d-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="2bf7d-150">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2bf7d-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="2bf7d-151">Monitorować wiadomości powitania bramy do chmury, ponieważ są one zapisywane tooAzure magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="2bf7d-152">*Szacowany czas toocomplete: 5 minut*</span><span class="sxs-lookup"><span data-stu-id="2bf7d-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="2bf7d-153">Przejdź za[odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2bf7d-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2bf7d-154">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="2bf7d-154">Troubleshooting</span></span>
<span data-ttu-id="2bf7d-155">Jeśli masz problemy podczas lekcje hello Szukaj rozwiązań w hello [Rozwiązywanie problemów](iot-hub-gateway-kit-c-sim-troubleshooting.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="2bf7d-156">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="2bf7d-156">Explore more</span></span>
<span data-ttu-id="2bf7d-157">Odwiedź hello [strefy developer Kit bramy IoT Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="2bf7d-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
