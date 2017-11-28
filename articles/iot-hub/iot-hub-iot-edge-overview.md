---
title: "Omówienie usługi Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Opisano podstawowe pojęcia architektury w programie Azure IoT Edge, takie jak bramy, moduły i brokerów."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="ca821-103">Azure IoT krawędzi architektury pojęcia.</span><span class="sxs-lookup"><span data-stu-id="ca821-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="ca821-104">Przed sprawdzić wszelkie przykładowy kod lub utworzyć własne pole bramę, używając krawędzi IoT, zapoznaj się podstawowe pojęcia, które stanowi podstawę do architektury IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="ca821-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="ca821-105">Moduły krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="ca821-105">IoT Edge modules</span></span>

<span data-ttu-id="ca821-106">Tworzenie bramy Azure IoT krawędzi, tworząc i składanie *modułów krawędzi IoT*.</span><span class="sxs-lookup"><span data-stu-id="ca821-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="ca821-107">Moduły wymieniają między sobą dane za pomocą *komunikatów*.</span><span class="sxs-lookup"><span data-stu-id="ca821-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="ca821-108">Moduł odbiera komunikat, wykonuje na nim jakąś akcję, opcjonalnie przekształca go w nowy komunikat, a następnie publikuje go w celu przetworzenia przez inne moduły.</span><span class="sxs-lookup"><span data-stu-id="ca821-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="ca821-109">Niektóre moduły mogą jedynie tworzyć nowe komunikaty i nigdy nie przetwarzają komunikatów przychodzących.</span><span class="sxs-lookup"><span data-stu-id="ca821-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="ca821-110">Łańcuch modułów tworzy potok przetwarzania danych, w którym każdy moduł wykonuje przekształcenie danych w jednym punkcie tego potoku.</span><span class="sxs-lookup"><span data-stu-id="ca821-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Łańcuch modułów w bramie utworzonej przy użyciu usługi Azure IoT Edge][1]

<span data-ttu-id="ca821-112">Krawędź IoT zawiera następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="ca821-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="ca821-113">Moduły wstępnie napisane wykonać typowe funkcje bramy.</span><span class="sxs-lookup"><span data-stu-id="ca821-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="ca821-114">Interfejsy, za pomocą których deweloperzy mogą pisać moduły niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="ca821-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="ca821-115">Infrastruktura niezbędna do wdrożenia i uruchomienia zestawu modułów.</span><span class="sxs-lookup"><span data-stu-id="ca821-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="ca821-116">Zestaw SDK udostępnia warstwę abstrakcji, która umożliwia tworzenie bramy do uruchamiania na różnych systemów operacyjnych i platform.</span><span class="sxs-lookup"><span data-stu-id="ca821-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Warstwa abstrakcji usługi Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="ca821-118">Komunikaty</span><span class="sxs-lookup"><span data-stu-id="ca821-118">Messages</span></span>

<span data-ttu-id="ca821-119">Wyobrażenie modułów przekazujących sobie nawzajem komunikaty ułatwia zrozumienie sposobu działania bramy, jednak nie odzwierciedla precyzyjnie tego procesu.</span><span class="sxs-lookup"><span data-stu-id="ca821-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="ca821-120">Moduły krawędzi IoT umożliwia broker komunikują się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="ca821-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="ca821-121">Moduły publikowania komunikatów brokera (przy użyciu wzorce obsługi komunikatów, takie jak magistrala lub publikowania/subskrypcji), a następnie umożliwił brokera kierowania wiadomości z modułów dołączone do niego.</span><span class="sxs-lookup"><span data-stu-id="ca821-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="ca821-122">Moduł publikuje komunikaty do brokera przy użyciu funkcji **Broker_Publish**.</span><span class="sxs-lookup"><span data-stu-id="ca821-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="ca821-123">Broker dostarcza komunikaty do modułu za pomocą funkcji wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="ca821-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="ca821-124">Komunikat składa się z zestawu właściwości klucz/wartość oraz zawartości przekazywanej w postaci bloku pamięci.</span><span class="sxs-lookup"><span data-stu-id="ca821-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Rola brokera w usłudze Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="ca821-126">Routing i filtrowanie komunikatów</span><span class="sxs-lookup"><span data-stu-id="ca821-126">Message routing and filtering</span></span>

<span data-ttu-id="ca821-127">Istnieją dwa sposoby do kierowania wiadomości z poprawną modułów krawędzi IoT:</span><span class="sxs-lookup"><span data-stu-id="ca821-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="ca821-128">Można przekazać zestawu łączy mogą zostać przekazane do brokera będzie wówczas traktował brokera źródłowy i odbiorczy dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="ca821-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="ca821-129">Moduł można filtrować według właściwości wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ca821-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="ca821-130">Moduł powinien podejmować działania dotyczące komunikatu tylko wtedy, gdy komunikat jest przeznaczony dla niego.</span><span class="sxs-lookup"><span data-stu-id="ca821-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="ca821-131">Łącza i efektywnie filtrowania wiadomości utworzyć potok wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ca821-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca821-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca821-132">Next steps</span></span>

<span data-ttu-id="ca821-133">Aby wyświetlić te pojęcia stosowane w próbce można uruchomić, zobacz [architektura Eksplorowanie usługi Azure IoT krawędzi][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="ca821-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md