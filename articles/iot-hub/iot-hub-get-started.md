---
title: "Centrum IoT Azure — wprowadzenie łączenie chmury toohello urządzenia IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect Twojego urządzenia IoT i starter Kit tooAzure Centrum IoT. Urządzenia można wysyłać dane telemetryczne tooIoT Centrum Centrum IoT można monitorować i zarządzania urządzeniami."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Samouczek Centrum Azure iot
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="b625f-105">Usługa Azure IoT Hub wprowadzenie samouczki</span><span class="sxs-lookup"><span data-stu-id="b625f-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="b625f-106">Można użyć Centrum IoT Azure i hello Azure IoT urządzenia zestawów SDK toobuild Internetu rzeczy (IoT) rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="b625f-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="b625f-107">Centrum IoT Azure jest w pełni zarządzana usługa w chmurze hello bezpieczny sposób łączy, monitoruje i zarządza urządzeniami IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="b625f-108">Użyj tooimplement zestawy SDK urządzenia IoT Azure hello urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="b625f-109">Użyj bramy IoT w bardziej złożonych scenariuszach IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="b625f-110">Na przykład, gdzie należy tooconsider czynników, takich jak starszych urządzeń, kosztów przepustowości, zasady zabezpieczeń i prywatności lub przetwarzania danych krawędzi.</span><span class="sxs-lookup"><span data-stu-id="b625f-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="b625f-111">W tych scenariuszach używasz tooimplement Azure IoT krawędzi bramy, która łączy się z Centrum IoT tooyour urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b625f-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="b625f-112">Samouczki hello pokrycia</span><span class="sxs-lookup"><span data-stu-id="b625f-112">What hello tutorials cover</span></span>

<span data-ttu-id="b625f-113">Te samouczki wprowadzenie tooAzure Centrum IoT i urządzeniami hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="b625f-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="b625f-114">Samouczki Hello obejmują typowe IoT scenariusze toodemonstrate hello funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="b625f-115">Witaj samouczki również ilustrują sposób toocombine Centrum IoT z platformy Azure, innych usług i narzędzi toobuild bardziej wydajne rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="b625f-116">W samouczkach hello można toouse symulowane lub rzeczywistego urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="b625f-117">Ponadto, aby dowiedzieć się jak toouse bramy tooenable urządzeń tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b625f-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="b625f-118">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="b625f-118">Set up your device</span></span>

<span data-ttu-id="b625f-119">Połącz IoT urządzenia lub bramy tooAzure Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="b625f-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="b625f-120">Możesz wybrać tooget fizycznego lub symulowane urządzenie, uruchomiona:</span><span class="sxs-lookup"><span data-stu-id="b625f-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="b625f-121">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="b625f-121">IoT device</span></span>                       | <span data-ttu-id="b625f-122">Język programowania</span><span class="sxs-lookup"><span data-stu-id="b625f-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="b625f-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b625f-123">Raspberry Pi</span></span>                     | <span data-ttu-id="b625f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="b625f-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="b625f-125">Zestaw deweloperski IoT</span><span class="sxs-lookup"><span data-stu-id="b625f-125">IoT DevKit</span></span>                       | <span data-ttu-id="b625f-126">[Arduino w VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="b625f-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="b625f-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="b625f-127">Intel Edison</span></span>                     | <span data-ttu-id="b625f-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="b625f-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="b625f-129">ESP8266 HUZZAH Adafruit piór</span><span class="sxs-lookup"><span data-stu-id="b625f-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="b625f-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="b625f-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="b625f-131">Sparkfun ESP8266 operacją deweloperów</span><span class="sxs-lookup"><span data-stu-id="b625f-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="b625f-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="b625f-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="b625f-133">M0 Adafruit piór</span><span class="sxs-lookup"><span data-stu-id="b625f-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="b625f-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="b625f-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="b625f-135">Symulowane urządzenie na komputerze</span><span class="sxs-lookup"><span data-stu-id="b625f-135">Simulated device on PC</span></span>           | <span data-ttu-id="b625f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [języka Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="b625f-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="b625f-137">Symulator urządzeń online</span><span class="sxs-lookup"><span data-stu-id="b625f-137">Online device simulator</span></span>         | <span data-ttu-id="b625f-138">[Pi malinowe (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="b625f-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="b625f-139">Ponadto można użyć Centrum IoT krawędzi bramy tooenable urządzeń tooconnect tooyour IoT:</span><span class="sxs-lookup"><span data-stu-id="b625f-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="b625f-140">Urządzenie bramy</span><span class="sxs-lookup"><span data-stu-id="b625f-140">Gateway device</span></span>               | <span data-ttu-id="b625f-141">Język programowania</span><span class="sxs-lookup"><span data-stu-id="b625f-141">Programming language</span></span> | <span data-ttu-id="b625f-142">Platforma</span><span class="sxs-lookup"><span data-stu-id="b625f-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="b625f-143">NUC firmy Intel (model DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="b625f-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="b625f-144">C</span><span class="sxs-lookup"><span data-stu-id="b625f-144">C</span></span>                    | <span data-ttu-id="b625f-145">[Rzeka knie systemu Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="b625f-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="b625f-146">Symulowane bramy</span><span class="sxs-lookup"><span data-stu-id="b625f-146">Simulated gateway</span></span>            | <span data-ttu-id="b625f-147">C</span><span class="sxs-lookup"><span data-stu-id="b625f-147">C</span></span>                    | <span data-ttu-id="b625f-148">[Linux][Sim_Lnx], [systemu Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="b625f-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
