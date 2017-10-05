---
title: Centrum IoT Azure skalowanie | Dokumentacja firmy Microsoft
description: "Jak skalować Centrum IoT do obsługi sieci przepływności przewidywanego wiadomości. Zawiera podsumowanie obsługiwana przepływność dla każdej warstwy i opcje dotyczące dzielenia na fragmenty."
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
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="96197-104">Skalować rozwiązania IoT hub</span><span class="sxs-lookup"><span data-stu-id="96197-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="96197-105">Centrum IoT Azure może obsługiwać do milionów równocześnie połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="96197-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="96197-106">Aby uzyskać więcej informacji, zobacz [Centrum IoT cennik][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="96197-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="96197-107">Każda jednostka Centrum IoT umożliwia pewną liczbę wiadomości codzienne.</span><span class="sxs-lookup"><span data-stu-id="96197-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="96197-108">Aby prawidłowo skalować rozwiązania, należy wziąć pod uwagę określonego korzystanie z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="96197-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="96197-109">W szczególności należy wziąć pod uwagę przepustowość wymagana szczytu w ramach następujących kategorii działań:</span><span class="sxs-lookup"><span data-stu-id="96197-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="96197-110">Komunikaty z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="96197-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="96197-111">Komunikaty chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="96197-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="96197-112">Operacje rejestru tożsamości</span><span class="sxs-lookup"><span data-stu-id="96197-112">Identity registry operations</span></span>

<span data-ttu-id="96197-113">Oprócz tych informacji przepływności, zobacz [Centrum IoT przydziały i limity] [ IoT Hub quotas and throttles] i odpowiednio zaprojektować rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="96197-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="96197-114">Przepustowość urządzenia do chmury i chmury do urządzenia wiadomości</span><span class="sxs-lookup"><span data-stu-id="96197-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="96197-115">Najlepszym sposobem rozmiaru rozwiązania IoT Hub jest do oceny ruchu na podstawie jednostkę.</span><span class="sxs-lookup"><span data-stu-id="96197-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="96197-116">Urządzenia do chmury wiadomości zgodna z tymi wytycznymi długoterminowa przepustowość.</span><span class="sxs-lookup"><span data-stu-id="96197-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="96197-117">Warstwa</span><span class="sxs-lookup"><span data-stu-id="96197-117">Tier</span></span> | <span data-ttu-id="96197-118">Długoterminowa przepustowość</span><span class="sxs-lookup"><span data-stu-id="96197-118">Sustained throughput</span></span> | <span data-ttu-id="96197-119">Wskaźnik wysyłania stałej</span><span class="sxs-lookup"><span data-stu-id="96197-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96197-120">S1</span><span class="sxs-lookup"><span data-stu-id="96197-120">S1</span></span> |<span data-ttu-id="96197-121">Maksymalnie 1111 KB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="96197-122">(1,5 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="96197-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="96197-123">Średnia 278 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="96197-124">(400 000 komunikatów/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="96197-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="96197-125">S2</span><span class="sxs-lookup"><span data-stu-id="96197-125">S2</span></span> |<span data-ttu-id="96197-126">Maksymalnie 16 MB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="96197-127">(22.8 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="96197-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="96197-128">Średnia 4,167 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="96197-129">(6 mln wiadomości/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="96197-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="96197-130">S3</span><span class="sxs-lookup"><span data-stu-id="96197-130">S3</span></span> |<span data-ttu-id="96197-131">Maksymalnie 814 MB na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="96197-132">(1144.4 GB/dzień/jednostka)</span><span class="sxs-lookup"><span data-stu-id="96197-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="96197-133">Średnia 208,333 komunikatów na minutę na jednostkę</span><span class="sxs-lookup"><span data-stu-id="96197-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="96197-134">(300 milionów wiadomości/dzień na jednostkę)</span><span class="sxs-lookup"><span data-stu-id="96197-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="96197-135">Przepływność operacji rejestru tożsamości</span><span class="sxs-lookup"><span data-stu-id="96197-135">Identity registry operation throughput</span></span>
<span data-ttu-id="96197-136">Operacje rejestru tożsamości Centrum IoT nie powinna być czasu wykonywania operacji, ponieważ przede wszystkim dotyczące inicjowania obsługi urządzeń.</span><span class="sxs-lookup"><span data-stu-id="96197-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="96197-137">Dla określonego serii numerów wydajności, zobacz [Centrum IoT przydziały i limity][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="96197-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="96197-138">Dzielenia na fragmenty</span><span class="sxs-lookup"><span data-stu-id="96197-138">Sharding</span></span>
<span data-ttu-id="96197-139">Podczas jednego centrum IoT można skalować do milionów urządzeń, czasami rozwiązanie wymaga charakterystyk wydajności właściwe, które nie może zagwarantować pojedynczego Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="96197-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="96197-140">W takim przypadku zaleca się partycji urządzenia do wielu centra IoT.</span><span class="sxs-lookup"><span data-stu-id="96197-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="96197-141">Centra IoT wielu smooth seria ruchu i uzyskiwanie wymagana przepustowość lub szybkości działania, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="96197-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96197-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96197-142">Next steps</span></span>
<span data-ttu-id="96197-143">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="96197-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="96197-144">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="96197-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="96197-145">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="96197-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
