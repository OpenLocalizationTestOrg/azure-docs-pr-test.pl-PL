---
title: "aaaOverview Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Opisano hello klucza architektury pojęcia w programie Azure IoT Edge takie jak bramy, moduły i brokerów."
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="811d6-103">Azure IoT krawędzi architektury pojęcia.</span><span class="sxs-lookup"><span data-stu-id="811d6-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="811d6-104">Przed sprawdzić wszelkie przykładowy kod lub utworzyć własne pole bramę, używając krawędzi IoT, zapoznaj się hello podstawowe pojęcia, które stanowi podstawę hello architektury IoT krawędzi.</span><span class="sxs-lookup"><span data-stu-id="811d6-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="811d6-105">Moduły krawędzi IoT</span><span class="sxs-lookup"><span data-stu-id="811d6-105">IoT Edge modules</span></span>

<span data-ttu-id="811d6-106">Tworzenie bramy Azure IoT krawędzi, tworząc i składanie *modułów krawędzi IoT*.</span><span class="sxs-lookup"><span data-stu-id="811d6-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="811d6-107">Użyj modułów *wiadomości* tooexchange danych ze sobą.</span><span class="sxs-lookup"><span data-stu-id="811d6-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="811d6-108">Moduł odbiera komunikat, wykonuje akcję na nim opcjonalnie przekształca je w nowej wiadomości i publikuje ją dla tooprocess innych modułów.</span><span class="sxs-lookup"><span data-stu-id="811d6-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="811d6-109">Niektóre moduły mogą jedynie tworzyć nowe komunikaty i nigdy nie przetwarzają komunikatów przychodzących.</span><span class="sxs-lookup"><span data-stu-id="811d6-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="811d6-110">Łańcuch modułów tworzy potoku przetwarzania danych z każdego modułu wykonania transformację na powitania danych w jednym punkcie w tym potoku.</span><span class="sxs-lookup"><span data-stu-id="811d6-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Łańcuch modułów w bramie utworzonej przy użyciu usługi Azure IoT Edge][1]

<span data-ttu-id="811d6-112">Krawędź IoT zawiera hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="811d6-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="811d6-113">Moduły wstępnie napisane wykonać typowe funkcje bramy.</span><span class="sxs-lookup"><span data-stu-id="811d6-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="811d6-114">interfejsy Hello a developer służy toowrite niestandardowe moduły.</span><span class="sxs-lookup"><span data-stu-id="811d6-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="811d6-115">Witaj toodeploy niezbędne infrastruktury, a następnie uruchom zestaw modułów.</span><span class="sxs-lookup"><span data-stu-id="811d6-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="811d6-116">Hello SDK udostępnia warstwę abstrakcji, która umożliwia toorun bram toobuild na różnych systemów operacyjnych i platform.</span><span class="sxs-lookup"><span data-stu-id="811d6-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Warstwa abstrakcji usługi Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="811d6-118">Komunikaty</span><span class="sxs-lookup"><span data-stu-id="811d6-118">Messages</span></span>

<span data-ttu-id="811d6-119">Chociaż planowanie modułów przekazywania wiadomości tooeach innych jest tooconceptualize wygodny sposób, w jaki sposób funkcje bramy, go nie odzwierciedlają dokładnie co się stanie.</span><span class="sxs-lookup"><span data-stu-id="811d6-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="811d6-120">Moduły krawędzi IoT Użyj toocommunicate brokera ze sobą.</span><span class="sxs-lookup"><span data-stu-id="811d6-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="811d6-121">Moduły publikowania komunikatów brokera toohello (przy użyciu wzorce obsługi komunikatów, takie jak magistrala lub publikowania/subskrypcji), a następnie zezwolić na powitania brokera trasy hello komunikat toohello modułów połączonych tooit.</span><span class="sxs-lookup"><span data-stu-id="811d6-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="811d6-122">Moduł używa hello **Broker_Publish** funkcji toopublish brokera toohello komunikatów.</span><span class="sxs-lookup"><span data-stu-id="811d6-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="811d6-123">Hello broker zapewnia moduł tooa wiadomości przez funkcję wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="811d6-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="811d6-124">Komunikat składa się z zestawu właściwości klucz/wartość oraz zawartości przekazywanej w postaci bloku pamięci.</span><span class="sxs-lookup"><span data-stu-id="811d6-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Rola Hello hello brokera w programie Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="811d6-126">Routing i filtrowanie komunikatów</span><span class="sxs-lookup"><span data-stu-id="811d6-126">Message routing and filtering</span></span>

<span data-ttu-id="811d6-127">Istnieją dwa sposoby toodirect wiadomości toohello poprawne krawędzi IoT modułów:</span><span class="sxs-lookup"><span data-stu-id="811d6-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="811d6-128">Można przekazać zestawu łączy mogą zostać przekazane brokera toohello będzie wówczas traktował brokera hello hello źródłowy i odbiorczy dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="811d6-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="811d6-129">Moduł można filtrować według właściwości hello wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="811d6-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="811d6-130">Moduł tylko powinien operować na komunikat, jeśli wiadomość hello jest przeznaczony dla niego.</span><span class="sxs-lookup"><span data-stu-id="811d6-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="811d6-131">Łącza i efektywnie filtrowania wiadomości utworzyć potok wiadomości.</span><span class="sxs-lookup"><span data-stu-id="811d6-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="811d6-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="811d6-132">Next steps</span></span>

<span data-ttu-id="811d6-133">Zobacz te pojęcia stosowane w próbce można uruchomić toosee [architektura Eksplorowanie usługi Azure IoT krawędzi][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="811d6-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md