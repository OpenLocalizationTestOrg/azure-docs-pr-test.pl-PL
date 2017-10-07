---
title: "aaaDefinine i zarządzania stanem w programie Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Jak toodefine i zarządzanie stanem usługi w sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="754f3-103">Stan usługi</span><span class="sxs-lookup"><span data-stu-id="754f3-103">Service state</span></span>
<span data-ttu-id="754f3-104">**Usługa stanu** odwołuje się toohello w pamięci lub na dysku danych, że usługa wymaga toofunction.</span><span class="sxs-lookup"><span data-stu-id="754f3-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="754f3-105">Obejmuje on, na przykład struktur danych hello zmienne Członkowskie usługi hello odczytuje i zapisuje toodo pracy.</span><span class="sxs-lookup"><span data-stu-id="754f3-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="754f3-106">W zależności od tego, jak usługa hello została zaprojektowana on może również obejmować plików lub innych zasobów, które są przechowywane na dysku.</span><span class="sxs-lookup"><span data-stu-id="754f3-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="754f3-107">Na przykład hello pliki bazy danych użyje toostore danych i dzienników transakcji.</span><span class="sxs-lookup"><span data-stu-id="754f3-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="754f3-108">Jako przykład usługi zastanówmy Kalkulator.</span><span class="sxs-lookup"><span data-stu-id="754f3-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="754f3-109">Kalkulator podstawowe usługi ma dwie liczby i zwraca ich sumę.</span><span class="sxs-lookup"><span data-stu-id="754f3-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="754f3-110">Wykonywanie tego obliczenia pociąga za sobą żadnych zmiennych Członkowskich lub inne informacje.</span><span class="sxs-lookup"><span data-stu-id="754f3-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="754f3-111">Teraz Rozważmy hello tego samego Kalkulator, ale z dodatkową metodę przechowywania i zwracanie hello ostatniego suma jest obliczana.</span><span class="sxs-lookup"><span data-stu-id="754f3-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="754f3-112">Ta usługa jest teraz stanowych.</span><span class="sxs-lookup"><span data-stu-id="754f3-112">This service is now stateful.</span></span> <span data-ttu-id="754f3-113">Wartość oznacza, że zawiera niektóre stan, który zapisuje toowhen oblicza sumę nowe i odczytuje z podczas poproś tooreturn hello ostatniego obliczona sum.</span><span class="sxs-lookup"><span data-stu-id="754f3-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="754f3-114">Sieć szkieletowa usług Azure hello pierwszej usługi nosi usługę bezstanową.</span><span class="sxs-lookup"><span data-stu-id="754f3-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="754f3-115">Usługa drugi Hello jest nazywany usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="754f3-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="754f3-116">Przechowywanie stanu usługi</span><span class="sxs-lookup"><span data-stu-id="754f3-116">Storing service state</span></span>
<span data-ttu-id="754f3-117">Stan można externalized lub wspólnie z kodem hello, który jest manipulowanie hello stanu.</span><span class="sxs-lookup"><span data-stu-id="754f3-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="754f3-118">Externalization stan jest zazwyczaj wykonywane za pomocą zewnętrznej bazy danych lub innych danych przechowywania, że działa na różnych komputerach za pośrednictwem sieci hello lub pozaprocesowa na hello tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="754f3-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="754f3-119">W naszym przykładzie Kalkulator magazynu danych hello można bazy danych SQL lub wystąpienie magazynu tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="754f3-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="754f3-120">Suma hello toocompute każdego żądania przeprowadzi aktualizację na tych danych i żądań toohello usługi tooreturn hello wartość doprowadzi do bieżącej wartości hello są pobierane z magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="754f3-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="754f3-121">Stan można także wspólnie z hello obsługujące hello stanu.</span><span class="sxs-lookup"><span data-stu-id="754f3-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="754f3-122">Stanowych usług w sieci szkieletowej usług są zazwyczaj tworzone przy użyciu tego modelu.</span><span class="sxs-lookup"><span data-stu-id="754f3-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="754f3-123">Usługa Service Fabric realizuje hello tooensure infrastruktury, że ten stan jest wysoko dostępnych, spójne i trwałe i że usługi hello wbudowane w ten sposób można łatwo skalować.</span><span class="sxs-lookup"><span data-stu-id="754f3-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="754f3-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="754f3-124">Next steps</span></span>
<span data-ttu-id="754f3-125">Aby uzyskać więcej informacji dotyczących pojęć sieci szkieletowej usług zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="754f3-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="754f3-126">Dostępność usług sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="754f3-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="754f3-127">Skalowalność usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="754f3-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="754f3-128">Partycjonowanie usług sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="754f3-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="754f3-129">Niezawodne usługi sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="754f3-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
