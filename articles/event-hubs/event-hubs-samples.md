---
title: "Przykłady usługi Event Hubs aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładów dla platformy Azure Event Hubs"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: f01f52e6c13f9e885999a6726143440bbc70446d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="ee962-103">Przykłady centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-103">Event Hubs samples</span></span> 

<span data-ttu-id="ee962-104">Hello zestaw próbek Azure Event Hubs przedstawiono kluczowe funkcje [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ee962-104">hello set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="ee962-105">W tym artykule kategoryzuje i opisano dostępne z łącza tooeach przykłady hello.</span><span class="sxs-lookup"><span data-stu-id="ee962-105">This article categorizes and describes hello samples available, with links tooeach.</span></span>

<span data-ttu-id="ee962-106">W czasie hello pisania tego dokumentu usługa Event Hubs przykłady znajdują się w kilku różnych miejscach:</span><span class="sxs-lookup"><span data-stu-id="ee962-106">At hello time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="ee962-107">Przykłady kodu dla deweloperów MSDN</span><span class="sxs-lookup"><span data-stu-id="ee962-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="ee962-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="ee962-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="ee962-109">Aby uzyskać więcej informacji o różnych wersji programu .NET Framework hello, zobacz [struktury i obiekty docelowe](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="ee962-109">For more information about different versions of hello .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="ee962-110">Więcej przykładów zostanie dodany wraz z upływem czasu, więc zaglądaj tu często aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ee962-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="ee962-111">.NET standard</span><span class="sxs-lookup"><span data-stu-id="ee962-111">.NET Standard</span></span>

<span data-ttu-id="ee962-112">Witaj poniższe przykłady pokazują, jak toosend i odbierania zdarzeń za pomocą hello [klienta usługi Event Hubs](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) dla hello [biblioteki .NET Standard](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="ee962-112">hello following samples demonstrate how toosend and receive events using hello [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for hello [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="ee962-113">Wysyłanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-113">Send events</span></span> 

<span data-ttu-id="ee962-114">Witaj [rozpocząć wysyłanie](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) przykładzie pokazano, jak toowrite .NET Core konsoli aplikacji, która wysyła zdarzenia tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ee962-114">hello [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how toowrite a .NET Core console application that sends events tooan event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="ee962-115">Odbieranie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-115">Receive events</span></span> 

<span data-ttu-id="ee962-116">Witaj [rozpocząć odbieranie z hello hosta procesora zdarzeń](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) próbka jest aplikacji konsoli .NET Core, który odbiera komunikaty z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ee962-116">hello [Get started receiving with hello Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using hello Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="ee962-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="ee962-117">.NET Framework</span></span>   

<span data-ttu-id="ee962-118">Te przykłady pokazują różnych funkcji usługi Azure Event hubs, przeznaczonych dla hello [Biblioteka programu .NET Framework](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="ee962-118">These samples demonstrate various other features of Azure Event Hubs, targeting hello [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="ee962-119">Powiadom użytkowników zdarzeń odebranych</span><span class="sxs-lookup"><span data-stu-id="ee962-119">Notify users of events received</span></span>

<span data-ttu-id="ee962-120">Witaj [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) próbki powiadamia użytkowników danych otrzymywanych z czujników lub innych systemów.</span><span class="sxs-lookup"><span data-stu-id="ee962-120">hello [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="ee962-121">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ee962-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="ee962-122">Witaj [Event Hubs wprowadzenie](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) przykładzie pokazano hello podstawowe możliwości usługi Event hubs, takich jak sposób wysyłania Centrum zdarzeń tooan zdarzenia toocreate Centrum zdarzeń i korzystanie ze zdarzeń przy użyciu hello [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="ee962-122">hello [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates hello basic capabilities of Event Hubs, such as how toocreate an event hub, send events tooan event hub, and consume events using hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="ee962-123">Skalowanie przetwarzania zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-123">Scale out event processing</span></span> 

<span data-ttu-id="ee962-124">Hello [skalowania przetwarzania zdarzeń](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) w przykładzie pokazano, jak toouse hello [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello obciążenie usługi Event Hubs strumienia zużycia.</span><span class="sxs-lookup"><span data-stu-id="ee962-124">hello [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how toouse hello [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="ee962-125">Widoczny jest sposób tooimplement hello **EventProcessor** i **EventProcessorFactory** strumienia zdarzeń hello toomanage obiektów.</span><span class="sxs-lookup"><span data-stu-id="ee962-125">It shows how tooimplement hello **EventProcessor** and **EventProcessorFactory** objects toomanage hello event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="ee962-126">Ściąganie danych z bazy danych SQL do Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="ee962-127">Witaj [SQL ściąganie danych](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) pokazano, jak dane toopull z SQL tabeli i wypchnąć go tooan Centrum zdarzeń, toouse jako dane wejściowe w podrzędnych analitycznych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee962-127">hello [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how toopull data from a SQL table and push it tooan event hub, toouse as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="ee962-128">Ściąganie danych sieci web do Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="ee962-129">Witaj [Importuj dane z sieci web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) pokazano, jak dane toopull zapobieganie publicznemu dostępowi do źródeł danych (na przykład Witaj informacje o ruchu stanowych tego źródła danych) i wypchnąć go tooan Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ee962-129">hello [Import data from hello web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how toopull data from public feeds (such as hello Department of Transportation's traffic information feed) and push it tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee962-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee962-130">Next steps</span></span>

<span data-ttu-id="ee962-131">Więcej informacji na temat wersji systemu .NET Framework, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="ee962-131">Learn more about .NET Framework versions by visiting hello following links:</span></span>

- [<span data-ttu-id="ee962-132">Struktury i cele</span><span class="sxs-lookup"><span data-stu-id="ee962-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="ee962-133">.NET framework 4.6 i 4.5</span><span class="sxs-lookup"><span data-stu-id="ee962-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="ee962-134">Użytkownik może dowiedzieć się więcej o centra zdarzeń w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ee962-134">You can learn more about Event Hubs in hello following articles:</span></span>

- [<span data-ttu-id="ee962-135">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ee962-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="ee962-136">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ee962-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="ee962-137">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="ee962-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)