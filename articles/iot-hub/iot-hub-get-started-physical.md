---
title: "Wprowadzenie do łączenia urządzeń fizycznych tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect fizycznych urządzeń i tablice tooAzure Centrum IoT. Urządzenia można wysyłać dane telemetryczne tooIoT Centrum Centrum IoT można monitorować i zarządzania urządzeniami."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Samouczek Centrum Azure iot
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="9e2bc-105">Centrum IoT Azure Rozpoczynanie pracy z samouczkami urządzeń fizycznych</span><span class="sxs-lookup"><span data-stu-id="9e2bc-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="9e2bc-106">Te samouczki wprowadzenie tooAzure Centrum IoT i urządzeniami hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="9e2bc-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="9e2bc-107">Samouczki Hello obejmują typowe IoT scenariusze toodemonstrate hello funkcji Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9e2bc-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="9e2bc-108">Witaj samouczki również ilustrują sposób toocombine Centrum IoT z platformy Azure, innych usług i narzędzi toobuild bardziej wydajne rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="9e2bc-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="9e2bc-109">Hello samouczki na liście hello następujących Pokaż tabeli można jak toocreate fizyczne urządzenia IoT.</span><span class="sxs-lookup"><span data-stu-id="9e2bc-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="9e2bc-110">Urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="9e2bc-110">IoT device</span></span>                       | <span data-ttu-id="9e2bc-111">Język programowania</span><span class="sxs-lookup"><span data-stu-id="9e2bc-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="9e2bc-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9e2bc-112">Raspberry Pi</span></span>                    | <span data-ttu-id="9e2bc-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="9e2bc-114">Zestaw deweloperski IoT</span><span class="sxs-lookup"><span data-stu-id="9e2bc-114">IoT DevKit</span></span>                      | <span data-ttu-id="9e2bc-115">[Arduino w VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="9e2bc-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="9e2bc-116">Intel Edison</span></span>                    | <span data-ttu-id="9e2bc-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="9e2bc-118">ESP8266 HUZZAH Adafruit piór</span><span class="sxs-lookup"><span data-stu-id="9e2bc-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="9e2bc-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="9e2bc-120">Sparkfun ESP8266 operacją deweloperów</span><span class="sxs-lookup"><span data-stu-id="9e2bc-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="9e2bc-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="9e2bc-122">M0 Adafruit piór</span><span class="sxs-lookup"><span data-stu-id="9e2bc-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="9e2bc-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="9e2bc-124">Ponadto można użyć Centrum IoT krawędzi bramy tooenable urządzeń tooconnect tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="9e2bc-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="9e2bc-125">Urządzenie bramy</span><span class="sxs-lookup"><span data-stu-id="9e2bc-125">Gateway device</span></span>               | <span data-ttu-id="9e2bc-126">Język programowania</span><span class="sxs-lookup"><span data-stu-id="9e2bc-126">Programming language</span></span> | <span data-ttu-id="9e2bc-127">Platforma</span><span class="sxs-lookup"><span data-stu-id="9e2bc-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="9e2bc-128">NUC firmy Intel (model DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="9e2bc-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="9e2bc-129">C</span><span class="sxs-lookup"><span data-stu-id="9e2bc-129">C</span></span>                    | <span data-ttu-id="9e2bc-130">[Rzeka knie systemu Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="9e2bc-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
