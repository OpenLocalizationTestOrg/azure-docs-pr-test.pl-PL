---
title: "Symulowane Pi malina do chmury (Node.js) - symulatora sieci web Pi malina Połącz z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Symulator web Pi malina nawiązać połączenia z Centrum IoT Azure pi malina do wysyłania danych do chmury platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Symulator malinowe pi, pi azure iot malinowe, Centrum iot malinowe pi, pi malinowe wysyłania danych do chmury, malinowe pi do chmury"
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 3b80bf35d6af91d5bdb196d97668dc0f837b92cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-online-simulator-to-azure-iot-hub-nodejs"></a><span data-ttu-id="f476d-104">Symulator online Pi malina nawiązać połączenia z Centrum IoT Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="f476d-104">Connect Raspberry Pi online simulator to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="f476d-105">W tym samouczku Rozpocznij od uczenia podstawy pracy z Pi malina symulatora online.</span><span class="sxs-lookup"><span data-stu-id="f476d-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="f476d-106">Następnie Dowiedz się jak bezproblemowo połączyć symulatora Pi do chmury przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f476d-106">You then learn how to seamlessly connect the Pi simulator to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="f476d-107">Jeśli masz urządzenia fizyczne, odwiedź stronę [połączyć Pi malina z Centrum IoT Azure](iot-hub-raspberry-pi-kit-node-get-started.md) rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="f476d-107">If you have physical devices, visit [Connect Raspberry Pi to Azure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) to get started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator to Azure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="f476d-108">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="f476d-108">What you do</span></span>

* <span data-ttu-id="f476d-109">Poznaj podstawy Pi malina symulatora online.</span><span class="sxs-lookup"><span data-stu-id="f476d-109">Learn the basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f476d-110">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-110">Create an IoT hub.</span></span>
* <span data-ttu-id="f476d-111">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="f476d-112">Uruchom przykładową aplikację na Pi, aby wysłać dane czujników symulowane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-112">Run a sample application on Pi to send simulated sensor data to your IoT hub.</span></span>

<span data-ttu-id="f476d-113">Symulowane Pi malina nawiązać połączenia z Centrum IoT utworzony.</span><span class="sxs-lookup"><span data-stu-id="f476d-113">Connect simulated Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="f476d-114">Następnie uruchom przykładową aplikację z symulatorem do generowania danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="f476d-114">Then you run a sample application with the simulator to generate sensor data.</span></span> <span data-ttu-id="f476d-115">Ponadto użytkownik wysyła dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-115">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f476d-116">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="f476d-116">What you learn</span></span>

* <span data-ttu-id="f476d-117">Sposób tworzenia Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f476d-117">How to create an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="f476d-118">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f476d-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f476d-119">Jak pracować z Pi malina symulatora online.</span><span class="sxs-lookup"><span data-stu-id="f476d-119">How to work with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="f476d-120">Jak wysyłać dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-120">How to send sensor data to your IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="f476d-121">Omówienie symulatora web Pi malina</span><span class="sxs-lookup"><span data-stu-id="f476d-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="f476d-122">Kliknij przycisk, aby uruchomić symulatora online malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f476d-122">Click the button to launch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="f476d-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Uruchomić symulatora malinowe Pi</a></span><span class="sxs-lookup"><span data-stu-id="f476d-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="f476d-124">Istnieją trzy obszary w symulatorze sieci web.</span><span class="sxs-lookup"><span data-stu-id="f476d-124">There are three areas in the web simulator.</span></span>
1. <span data-ttu-id="f476d-125">Obszar zestawu — obwodu domyślny jest czy Pi nawiązanie połączenia z czujnika BME280 i LED.</span><span class="sxs-lookup"><span data-stu-id="f476d-125">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="f476d-126">Obszar jest zablokowana w wersji zapoznawczej tak aktualnie nie może wykonać dostosowania.</span><span class="sxs-lookup"><span data-stu-id="f476d-126">The area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="f476d-127">Kodowanie obszar — edytora online kodu dla Ciebie do kodu z malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f476d-127">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="f476d-128">Domyślne przykładowej aplikacji umożliwia zbieranie danych czujnika z czujnika BME280 i wysyła do Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="f476d-128">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="f476d-129">Aplikacja jest w pełni zgodne z rzeczywistym Pi.</span><span class="sxs-lookup"><span data-stu-id="f476d-129">The application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="f476d-130">Okno konsoli zintegrowane - zawiera dane wyjściowe w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f476d-130">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="f476d-131">U góry tego okna istnieją trzy przyciski.</span><span class="sxs-lookup"><span data-stu-id="f476d-131">At the top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="f476d-132">**Uruchom** — uruchamianie aplikacji w obszarze kodowania.</span><span class="sxs-lookup"><span data-stu-id="f476d-132">**Run** - Run the application in the coding area.</span></span>
   * <span data-ttu-id="f476d-133">**Resetuj** — Resetuj kodowania obszaru do aplikacji przykładowej domyślne.</span><span class="sxs-lookup"><span data-stu-id="f476d-133">**Reset** - Reset the coding area to the default sample application.</span></span>
   * <span data-ttu-id="f476d-134">**Składanie/rozszerzanie** — po prawej stronie jest przycisk umożliwiające składanie/Rozwiń okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="f476d-134">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

> [!NOTE] 
<span data-ttu-id="f476d-135">Symulator web Pi malina jest teraz dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f476d-135">The Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="f476d-136">Chcielibyśmy usłyszeć głosu w [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f476d-136">We'd like to hear your voice in the [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="f476d-137">Kod źródłowy jest publiczny na [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="f476d-137">The source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Omówienie Pi symulatora online](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="f476d-139">Uruchom przykładową aplikację w symulatorze web Pi</span><span class="sxs-lookup"><span data-stu-id="f476d-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="f476d-140">W kodowania obszaru, upewnij się, że pracujesz nad domyślne przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f476d-140">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="f476d-141">Zastąp symbol zastępczy w wierszu 15 ciąg połączenia urządzenia Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-141">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="f476d-142">![Zastąp ciąg połączenia urządzenia](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="f476d-142">![Replace the device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="f476d-143">Kliknij przycisk **Uruchom** lub typ `npm start` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f476d-143">Click **Run** or type `npm start` to run the application.</span></span>


<span data-ttu-id="f476d-144">Powinny pojawić się następujące dane wyjściowe, który zawiera dane czujników i komunikaty, które są wysyłane do Centrum IoT ![dane wyjściowe — dane czujników wysłanych z Pi malina Centrum IoT](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="f476d-144">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub ![Output - sensor data sent from Raspberry Pi to your IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="f476d-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f476d-145">Next steps</span></span>

<span data-ttu-id="f476d-146">Uruchomiono przykładowej aplikacji do zbierania danych czujników i wysyłania go do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f476d-146">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
