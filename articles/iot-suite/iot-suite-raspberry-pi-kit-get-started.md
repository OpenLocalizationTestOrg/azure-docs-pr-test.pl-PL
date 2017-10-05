---
title: "Nawiązać malinowe Pi pakiet Azure IoT | Dokumentacja firmy Microsoft"
description: "Samouczki przy użyciu środowiska Node.js lub C ułatwiają używanie malina Pi 3 i zdalne monitorowanie rozwiązania pakiet IoT Microsoft Azure IoT Starter Kit. Możliwe jest wybranie samouczek, która symuluje telemetrii, używającą rzeczywistych czujników lub aktualizacje oprogramowania układowego zdalnego, który umożliwia."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="f2dbb-104">Nawiązać połączenie zdalne rozwiązanie monitorowania programu Microsoft Azure IoT malina Pi 3 Starter Kit</span><span class="sxs-lookup"><span data-stu-id="f2dbb-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="f2dbb-105">W tej sekcji samouczki zapoznawania się sposób podłączania urządzeń malina Pi 3 do zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="f2dbb-106">Wybierz odpowiednie do preferowany język programowania samouczek i czy masz dostępne do użycia z Twojej Pi malina sprzętu czujnika.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="f2dbb-107">Samouczków</span><span class="sxs-lookup"><span data-stu-id="f2dbb-107">The tutorials</span></span>

| <span data-ttu-id="f2dbb-108">Samouczek</span><span class="sxs-lookup"><span data-stu-id="f2dbb-108">Tutorial</span></span> | <span data-ttu-id="f2dbb-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f2dbb-109">Notes</span></span> | <span data-ttu-id="f2dbb-110">Języki</span><span class="sxs-lookup"><span data-stu-id="f2dbb-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="f2dbb-111">Symulowane telemetrii (Basic)</span><span class="sxs-lookup"><span data-stu-id="f2dbb-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="f2dbb-112">Symuluje danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-112">Simulates sensor data.</span></span> <span data-ttu-id="f2dbb-113">Używa autonomicznej malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="f2dbb-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="f2dbb-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="f2dbb-115">Czujnik rzeczywistych (średni)</span><span class="sxs-lookup"><span data-stu-id="f2dbb-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="f2dbb-116">Używa danych z czujnika BME280 podłączone do sieci malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="f2dbb-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="f2dbb-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="f2dbb-118">Wdrożenie aktualizacji oprogramowania układowego (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="f2dbb-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="f2dbb-119">Używa danych z czujnika BME280 podłączone do sieci malina Pi.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="f2dbb-120">Włącza aktualizacje oprogramowania układowego zdalnego na użytkownika Pi malina.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="f2dbb-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="f2dbb-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f2dbb-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2dbb-122">Next steps</span></span>

<span data-ttu-id="f2dbb-123">Odwiedź stronę [Centrum deweloperów systemu Azure IoT](https://azure.microsoft.com/develop/iot/) więcej przykłady i dokumentacja Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="f2dbb-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md