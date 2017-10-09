---
title: "aaaSimulated Pi malina toocloud (Node.js) - tooAzure symulatora web Pi malina połączenia Centrum IoT | Dokumentacja firmy Microsoft"
description: "Połączenia sieci web Pi malina symulatora tooAzure Centrum IoT dla Pi malina toosend danych toohello chmury Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi malinowe symulatora azure iot malinowe pi malinowe pi Centrum iot, malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="5153c-104">Połącz tooAzure online symulatora Pi malina Centrum IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="5153c-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="5153c-105">W tym samouczku Rozpocznij od uczenia hello podstawy pracy z Pi malina symulatora online.</span><span class="sxs-lookup"><span data-stu-id="5153c-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="5153c-106">Następnie dowiesz się, jak połączyć tooseamlessly hello Pi symulatora toohello chmury za pomocą [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5153c-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="5153c-107">Jeśli masz urządzenia fizyczne, odwiedź stronę [tooAzure połączyć Pi malina Centrum IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5153c-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="5153c-108">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="5153c-108">What you do</span></span>

* <span data-ttu-id="5153c-109">Dowiedz się hello podstawy Pi malina symulatora online.</span><span class="sxs-lookup"><span data-stu-id="5153c-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="5153c-110">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5153c-110">Create an IoT hub.</span></span>
* <span data-ttu-id="5153c-111">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5153c-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="5153c-112">Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend symulowane Pi.</span><span class="sxs-lookup"><span data-stu-id="5153c-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="5153c-113">Połącz symulowane Pi malina tooan Centrum IoT utworzony.</span><span class="sxs-lookup"><span data-stu-id="5153c-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="5153c-114">Następnie uruchom przykładową aplikację z danych czujnika toogenerate symulatora hello.</span><span class="sxs-lookup"><span data-stu-id="5153c-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="5153c-115">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="5153c-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="5153c-116">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="5153c-116">What you learn</span></span>

* <span data-ttu-id="5153c-117">Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5153c-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="5153c-118">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="5153c-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5153c-119">Jak toowork z symulatorem online malina Pi.</span><span class="sxs-lookup"><span data-stu-id="5153c-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="5153c-120">Jak Centrum IoT tooyour danych czujnika toosend.</span><span class="sxs-lookup"><span data-stu-id="5153c-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="5153c-121">Omówienie symulatora web Pi malina</span><span class="sxs-lookup"><span data-stu-id="5153c-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="5153c-122">Kliknij przycisk hello przycisk toolaunch Pi malina online symulatora.</span><span class="sxs-lookup"><span data-stu-id="5153c-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
[<span data-ttu-id="5153c-123">Uruchomić symulatora Pi malina</span><span class="sxs-lookup"><span data-stu-id="5153c-123">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

<span data-ttu-id="5153c-124">Istnieją trzy obszary w symulatorze web hello.</span><span class="sxs-lookup"><span data-stu-id="5153c-124">There are three areas in hello web simulator.</span></span>
* <span data-ttu-id="5153c-125">Obszar zestawu — hello domyślne obwód jest, że Pi nawiązanie połączenia z czujnika BME280 i LED.</span><span class="sxs-lookup"><span data-stu-id="5153c-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="5153c-126">obszar Hello jest zablokowany w wersji preview tak aktualnie nie może wykonać dostosowania.</span><span class="sxs-lookup"><span data-stu-id="5153c-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
* <span data-ttu-id="5153c-127">Kodowanie obszar — edytora online kodu dla toocode z malina Pi.</span><span class="sxs-lookup"><span data-stu-id="5153c-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="5153c-128">Hello domyślne przykładowej aplikacji ułatwia toocollect danych czujnika z czujnika BME280 i wysyła tooyour Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="5153c-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="5153c-129">Aplikacja Hello jest w pełni zgodny z rzeczywistych urządzeń Pi.</span><span class="sxs-lookup"><span data-stu-id="5153c-129">hello application is fully compatible with real Pi devices.</span></span> 
* <span data-ttu-id="5153c-130">Okno konsoli zintegrowane - zawiera dane wyjściowe hello kodu.</span><span class="sxs-lookup"><span data-stu-id="5153c-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="5153c-131">U góry hello tego okna istnieją trzy przyciski.</span><span class="sxs-lookup"><span data-stu-id="5153c-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="5153c-132">**Uruchom** -uruchamiania aplikacji hello w hello kodowania obszaru.</span><span class="sxs-lookup"><span data-stu-id="5153c-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="5153c-133">**Resetuj** -kodowania obszaru toohello domyślne Przykładowa aplikacja hello resetowania.</span><span class="sxs-lookup"><span data-stu-id="5153c-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="5153c-134">**Składanie/rozszerzanie** — na powitania prawej stronie jest przycisk dla można rozwinąć/toofold hello okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="5153c-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="5153c-135">Symulator web Pi malina Hello jest teraz dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="5153c-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="5153c-136">Chcielibyśmy toohear głosu w hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="5153c-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="5153c-137">Kod źródłowy Hello jest publiczny na [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="5153c-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Omówienie Pi symulatora online](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="5153c-139">Uruchom przykładową aplikację w symulatorze web Pi</span><span class="sxs-lookup"><span data-stu-id="5153c-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="5153c-140">W kodowania obszaru, upewnij się, że pracujesz na powitania domyślne przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5153c-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="5153c-141">Zastąp symbol zastępczy hello w wierszu 15 hello ciąg połączenia urządzenia Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="5153c-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="5153c-142">![Zastąp ciąg połączenia urządzenia hello](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="5153c-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="5153c-143">Kliknij przycisk **Uruchom** lub typ `npm start` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5153c-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="5153c-144">Powinny pojawić się hello następujące dane wyjściowe, który zawiera dane czujników hello i wiadomości powitania, które są wysyłane z Centrum IoT tooyour ![dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="5153c-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="5153c-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5153c-145">Next steps</span></span>

<span data-ttu-id="5153c-146">Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5153c-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
