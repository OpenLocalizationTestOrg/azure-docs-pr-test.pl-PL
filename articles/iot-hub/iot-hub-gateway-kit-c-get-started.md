---
title: "Urządzeń Sensor tag & brama IoT Azure — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z IoT bramy Starter Kit, utworzenie Centrum Azure IoT i połącz Centrum IoT toohello Sensor tag i bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centrum Azure iot, bramy iot, wprowadzenie hello internet rzeczy, iot toolkit
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="43eee-104">Rozpoczynanie pracy z IoT bramy Starter Kit z Sensor tag</span><span class="sxs-lookup"><span data-stu-id="43eee-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43eee-105">Sensor tag</span><span class="sxs-lookup"><span data-stu-id="43eee-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="43eee-106">Symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="43eee-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="43eee-107">W tym samouczku, rozpoczyna się od uczenia hello podstawowe informacje dotyczące pracy z [IoT bramy Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="43eee-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="43eee-108">Możesz pracować z NUC firmy Intel, z systemem Linux rzeki knie i hello [Sensor tag analizy czasowej](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="43eee-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="43eee-109">Dowiesz się, jak połączyć tooseamleesly chmury toohello urządzeń przy użyciu Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="43eee-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="43eee-110">**Zestaw nie ma jeszcze?:** kliknij [tutaj](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="43eee-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="43eee-111">**Nie masz Sensor tag?:** [zaczynać się symulowane urządzenie](iot-hub-gateway-kit-c-sim-get-started.md) lub [kupić Sensor tag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="43eee-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="43eee-112">Lekcja 1. Konfigurowanie urządzenia NUC</span><span class="sxs-lookup"><span data-stu-id="43eee-112">Lesson 1: Configure your NUC</span></span>
![Diagram end-to-end Lesson1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="43eee-114">W tej lekcji w hello zestawu jako bramy usługi Azure IoT ustawiona NUC firmy Intel (dalej jednostki z przetwarzania danych), zainstaluj pakiet Azure IoT krawędzi hello na NUC i uruchom funkcję bramy hello tooverify przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43eee-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="43eee-115">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="43eee-116">Przejdź do zbyt[Konfigurowanie NUC Intel jako brama IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="43eee-117">Lekcja 2. Tworzenie centrum IoT Hub</span><span class="sxs-lookup"><span data-stu-id="43eee-117">Lesson 2: Create your IoT Hub</span></span>
![Diagram end-to-end Lesson2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="43eee-119">W tej lekcji należy zainstalować narzędzia hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="43eee-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="43eee-120">Następnie możesz utworzyć bezpłatne konto platformy Azure, udostępnić Centrum Azure IoT i utworzyć pierwszego urządzenia w Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="43eee-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="43eee-121">Lekcja 1 należy wykonać przed rozpoczęciem tej lekcji.</span><span class="sxs-lookup"><span data-stu-id="43eee-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="43eee-122">Pobierz narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="43eee-122">Get hello tools</span></span>
<span data-ttu-id="43eee-123">Zainstaluj narzędzia hello i oprogramowania na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="43eee-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="43eee-124">*Szacowany czas toocomplete: 20 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="43eee-125">Przejdź do zbyt[hello narzędzia](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="43eee-126">Tworzenie Centrum IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="43eee-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="43eee-127">Tworzenie grupy zasobów, obsługi administracyjnej pierwszego Centrum Azure IoT, a następnie dodaj Centrum IoT pierwszy toohello urządzenia przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43eee-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="43eee-128">*Szacowany czas toocomplete: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="43eee-129">Przejdź do zbyt[tworzenia Centrum IoT i rejestrowanie urządzenia](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="43eee-130">Lekcja 3: Odbieranie komunikatów z Sensor tag i odbieranie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="43eee-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="43eee-131">W tej lekcji użyjesz konfiguracji hello tooautomate skrypty i wykonywanie cz przykładową aplikację w Centrum.</span><span class="sxs-lookup"><span data-stu-id="43eee-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="43eee-132">Takie aplikacje używać kolekcji bezpiecznych modułów tooaggregate i przekształcania danych, przetwarzanie poleceń lub wykonać dowolną liczbę powiązanych zadań.</span><span class="sxs-lookup"><span data-stu-id="43eee-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="43eee-133">Moduły komunikować się ze sobą za pośrednictwem brokera komunikatów.</span><span class="sxs-lookup"><span data-stu-id="43eee-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="43eee-134">Witaj przykładowej aplikacji ma moduł cz i moduł Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="43eee-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="43eee-135">Moduł cz Hello odbiera dane z cz Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="43eee-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="43eee-136">Witaj pakietów hello danych odebranych i wysyła je Centrum IoT tooyour za pośrednictwem hello bramy struktura dostępna w programie Azure IoT Edge modułu Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="43eee-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagram end-to-end Lekcja 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="43eee-138">Konfigurowanie i uruchamianie hello cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="43eee-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="43eee-139">Konfigurowanie hello łączność między Sensor tag i bramy.</span><span class="sxs-lookup"><span data-stu-id="43eee-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="43eee-140">Następnie Zakończ hello konfiguracji i uruchom hello cz przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43eee-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="43eee-141">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="43eee-142">Przejdź do zbyt[Konfigurowanie i wykonywania hello cz przykładową aplikację](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="43eee-143">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="43eee-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="43eee-144">Uruchom przykładowy kod na hoście komputer tooread komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="43eee-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="43eee-145">*Szacowany czas toocomplete: 15 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="43eee-146">Przejdź do zbyt[odczytywać wiadomości z Centrum IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="43eee-147">Lekcja 4: Zapisywanie wiadomości tooAzure magazynu tabel</span><span class="sxs-lookup"><span data-stu-id="43eee-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="43eee-148">Utwórz aplikację Azure funkcja, która pobiera komunikaty przychodzące z Centrum IoT i zapisuje je w magazynie tabel tooAzure.</span><span class="sxs-lookup"><span data-stu-id="43eee-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagram end-to-end lekcji 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="43eee-150">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="43eee-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="43eee-151">Toocreate szablonu usługi Azure Resource Manager za pomocą aplikacji funkcji platformy Azure i konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="43eee-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="43eee-152">*Szacowany czas toocomplete: 10 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="43eee-153">Przejdź do zbyt[utworzyć konto magazynu Azure i aplikacji Azure — funkcja](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="43eee-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="43eee-154">Odczytywanie wiadomości utrwalone w magazynie tabel platformy Azure</span><span class="sxs-lookup"><span data-stu-id="43eee-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="43eee-155">Monitorować wiadomości powitania bramy do chmury, ponieważ są one zapisywane tooAzure magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="43eee-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="43eee-156">*Szacowany czas toocomplete: 5 minut*</span><span class="sxs-lookup"><span data-stu-id="43eee-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="43eee-157">Przejdź za[odczytywanie wiadomości utrwalane w magazynie tabel Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="43eee-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="43eee-158">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="43eee-158">Troubleshooting</span></span>
<span data-ttu-id="43eee-159">Jeśli masz problemy podczas lekcje hello Szukaj rozwiązań w hello [Rozwiązywanie problemów](iot-hub-gateway-kit-c-troubleshooting.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="43eee-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="43eee-160">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="43eee-160">Explore more</span></span>
<span data-ttu-id="43eee-161">Odwiedź hello [strefy developer Kit bramy IoT Intel](http://software.intel.com/iot/microsoft-azure) toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="43eee-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
