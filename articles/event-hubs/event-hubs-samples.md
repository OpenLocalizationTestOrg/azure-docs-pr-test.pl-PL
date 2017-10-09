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
# <a name="event-hubs-samples"></a>Przykłady centra zdarzeń 

Hello zestaw próbek Azure Event Hubs przedstawiono kluczowe funkcje [Azure Event Hubs](/azure/event-hubs/). W tym artykule kategoryzuje i opisano dostępne z łącza tooeach przykłady hello.

W czasie hello pisania tego dokumentu usługa Event Hubs przykłady znajdują się w kilku różnych miejscach:

- [Przykłady kodu dla deweloperów MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Aby uzyskać więcej informacji o różnych wersji programu .NET Framework hello, zobacz [struktury i obiekty docelowe](/dotnet/articles/standard/frameworks).

Więcej przykładów zostanie dodany wraz z upływem czasu, więc zaglądaj tu często aktualizacji.

## <a name="net-standard"></a>.NET standard

Witaj poniższe przykłady pokazują, jak toosend i odbierania zdarzeń za pomocą hello [klienta usługi Event Hubs](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) dla hello [biblioteki .NET Standard](/dotnet/articles/standard/library).

### <a name="send-events"></a>Wysyłanie zdarzeń 

Witaj [rozpocząć wysyłanie](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) przykładzie pokazano, jak toowrite .NET Core konsoli aplikacji, która wysyła zdarzenia tooan zdarzenia koncentratora.

### <a name="receive-events"></a>Odbieranie zdarzeń 

Witaj [rozpocząć odbieranie z hello hosta procesora zdarzeń](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) próbka jest aplikacji konsoli .NET Core, który odbiera komunikaty z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.

## <a name="net-framework"></a>.NET framework   

Te przykłady pokazują różnych funkcji usługi Azure Event hubs, przeznaczonych dla hello [Biblioteka programu .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Powiadom użytkowników zdarzeń odebranych

Witaj [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) próbki powiadamia użytkowników danych otrzymywanych z czujników lub innych systemów.

### <a name="get-started-with-event-hubs"></a>Rozpoczynanie pracy z usługą Event Hubs 

Witaj [Event Hubs wprowadzenie](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) przykładzie pokazano hello podstawowe możliwości usługi Event hubs, takich jak sposób wysyłania Centrum zdarzeń tooan zdarzenia toocreate Centrum zdarzeń i korzystanie ze zdarzeń przy użyciu hello [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Skalowanie przetwarzania zdarzeń 

Hello [skalowania przetwarzania zdarzeń](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) w przykładzie pokazano, jak toouse hello [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) toodistribute hello obciążenie usługi Event Hubs strumienia zużycia. Widoczny jest sposób tooimplement hello **EventProcessor** i **EventProcessorFactory** strumienia zdarzeń hello toomanage obiektów. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Ściąganie danych z bazy danych SQL do Centrum zdarzeń

Witaj [SQL ściąganie danych](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) pokazano, jak dane toopull z SQL tabeli i wypchnąć go tooan Centrum zdarzeń, toouse jako dane wejściowe w podrzędnych analitycznych aplikacji.

### <a name="pull-web-data-into-an-event-hub"></a>Ściąganie danych sieci web do Centrum zdarzeń 

Witaj [Importuj dane z sieci web hello](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) pokazano, jak dane toopull zapobieganie publicznemu dostępowi do źródeł danych (na przykład Witaj informacje o ruchu stanowych tego źródła danych) i wypchnąć go tooan Centrum zdarzeń.

## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat wersji systemu .NET Framework, przechodząc na stronę hello następującego łącza:

- [Struktury i cele](/dotnet/articles/standard/frameworks)
- [.NET framework 4.6 i 4.5](/dotnet/framework/index)

Użytkownik może dowiedzieć się więcej o centra zdarzeń w hello następujące artykuły:

- [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
- [Tworzenie centrum zdarzeń](event-hubs-create.md)
- [Event Hubs — często zadawane pytania](event-hubs-faq.md)