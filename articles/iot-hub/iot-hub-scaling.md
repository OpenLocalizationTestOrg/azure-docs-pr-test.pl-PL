---
title: Skalowanie Centrum IoT aaaAzure | Dokumentacja firmy Microsoft
description: "Jak tooscale Twojego toosupport Centrum IoT z przepływności przewidywanego wiadomości. Zawiera podsumowanie hello obsługiwana przepływność dla każdej warstwy i opcje dotyczące dzielenia na fragmenty."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="e5ed1-104">Skalować rozwiązania IoT hub</span><span class="sxs-lookup"><span data-stu-id="e5ed1-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="e5ed1-105">Centrum IoT Azure może obsługiwać tooa milionów jednocześnie podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="e5ed1-106">Aby uzyskać więcej informacji, zobacz [Centrum IoT cennik][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="e5ed1-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="e5ed1-107">Każda jednostka Centrum IoT umożliwia pewną liczbę wiadomości codzienne.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="e5ed1-108">tooproperly skalować rozwiązania należy wziąć pod uwagę określonego korzystanie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="e5ed1-109">W szczególności należy wziąć pod uwagę przepływności szczytu hello wymagane hello następujące kategorie działań:</span><span class="sxs-lookup"><span data-stu-id="e5ed1-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="e5ed1-110">Komunikaty z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="e5ed1-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="e5ed1-111">Komunikaty chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="e5ed1-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="e5ed1-112">Operacje rejestru tożsamości</span><span class="sxs-lookup"><span data-stu-id="e5ed1-112">Identity registry operations</span></span>

<span data-ttu-id="e5ed1-113">W dodatkowych toothis przepływności informacji, zobacz [Centrum IoT przydziały i limity] [ IoT Hub quotas and throttles] i odpowiednio zaprojektować rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="e5ed1-114">Przepustowość urządzenia do chmury i chmury do urządzenia wiadomości</span><span class="sxs-lookup"><span data-stu-id="e5ed1-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="e5ed1-115">Hello najlepsze sposób toosize rozwiązania IoT Hub jest tooevaluate hello ruchu na podstawie jednostkę.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="e5ed1-116">Urządzenia do chmury wiadomości zgodna z tymi wytycznymi długoterminowa przepustowość.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="e5ed1-117">Warstwa</span><span class="sxs-lookup"><span data-stu-id="e5ed1-117">Tier</span></span> | <span data-ttu-id="e5ed1-118">Długoterminowa przepustowość</span><span class="sxs-lookup"><span data-stu-id="e5ed1-118">Sustained throughput</span></span> | <span data-ttu-id="e5ed1-119">Wskaźnik wysyłania stałej</span><span class="sxs-lookup"><span data-stu-id="e5ed1-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5ed1-120">S1</span><span class="sxs-lookup"><span data-stu-id="e5ed1-120">S1</span></span> |<span data-ttu-id="e5ed1-121">Zapasowej too1111 KB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="e5ed1-122">(1,5 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="e5ed1-123">Średnia 278 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="e5ed1-124">(400 000 komunikatów/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="e5ed1-125">S2</span><span class="sxs-lookup"><span data-stu-id="e5ed1-125">S2</span></span> |<span data-ttu-id="e5ed1-126">Zapasowej too16 MB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="e5ed1-127">(22.8 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="e5ed1-128">Średnia 4,167 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="e5ed1-129">(6 mln wiadomości/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="e5ed1-130">S3</span><span class="sxs-lookup"><span data-stu-id="e5ed1-130">S3</span></span> |<span data-ttu-id="e5ed1-131">Zapasowej too814 MB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="e5ed1-132">(1144.4 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="e5ed1-133">Średnia 208,333 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="e5ed1-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="e5ed1-134">(300 milionów wiadomości/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="e5ed1-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="e5ed1-135">Przepływność operacji rejestru tożsamości</span><span class="sxs-lookup"><span data-stu-id="e5ed1-135">Identity registry operation throughput</span></span>
<span data-ttu-id="e5ed1-136">Operacje rejestru tożsamości Centrum IoT nie powinni toobe czasu wykonywania operacji, ponieważ są one przede wszystkim pokrewne toodevice inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="e5ed1-137">Dla określonego serii numerów wydajności, zobacz [Centrum IoT przydziały i limity][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="e5ed1-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="e5ed1-138">Dzielenia na fragmenty</span><span class="sxs-lookup"><span data-stu-id="e5ed1-138">Sharding</span></span>
<span data-ttu-id="e5ed1-139">Podczas jednego centrum IoT można skalować toomillions urządzenia, czasami rozwiązanie wymaga charakterystyk wydajności zależnych, które pojedynczego Centrum IoT nie może zagwarantować.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="e5ed1-140">W takim przypadku zaleca się partycji urządzenia do wielu centra IoT.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="e5ed1-141">Centra IoT wielu smooth seria ruchu i uzyskiwanie przepustowość wymagana hello lub szybkości działania, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="e5ed1-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5ed1-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5ed1-142">Next steps</span></span>
<span data-ttu-id="e5ed1-143">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e5ed1-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e5ed1-144">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="e5ed1-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="e5ed1-145">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e5ed1-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
