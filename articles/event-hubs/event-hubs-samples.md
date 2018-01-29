---
title: "Przykładów dla platformy Azure Event Hubs | Dokumentacja firmy Microsoft"
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
ms.date: 12/19/2017
ms.author: sethm
ms.openlocfilehash: 0af3f6bc6e074fae4d830f163419d6437d04e2df
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="event-hubs-samples"></a>Przykłady centra zdarzeń 

Zestaw przykładów Azure Event Hubs przedstawiono kluczowe funkcje [Azure Event Hubs](/azure/event-hubs/). W tym artykule kategoryzuje i opisano dostępne z łączami do każdego próbek.

W momencie pisania tego dokumentu usługa Event Hubs przykłady znajdują się w kilku różnych miejscach:

- [Przykłady kodu dla deweloperów MSDN](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Aby uzyskać więcej informacji o różnych wersjach programu .NET Framework, zobacz [struktury i obiekty docelowe](/dotnet/articles/standard/frameworks).

Więcej przykładów zostanie dodany wraz z upływem czasu, więc zaglądaj tu często aktualizacji.

## <a name="net-standard"></a>.NET standard

Poniższe przykłady przedstawiają sposób wysyłania i odbierania zdarzeń za pomocą [klienta usługi Event Hubs](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) dla [biblioteki .NET Standard](/dotnet/articles/standard/library).

### <a name="send-events"></a>Wysyłanie zdarzeń 

[Rozpocząć wysyłanie](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) przykład przedstawia sposób zapisania aplikacji konsoli .NET Core, która wysyła zdarzenia do Centrum zdarzeń.

### <a name="receive-events"></a>Odbieranie zdarzeń 

[Rozpocząć odbieranie z hosta procesora zdarzeń](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) próbka jest aplikacji konsoli .NET Core, który odbiera komunikaty z Centrum zdarzeń przy użyciu hosta procesora zdarzeń.

## <a name="net-framework"></a>.NET framework   

Te przykłady pokazują różnych funkcji usługi Azure Event hubs, przeznaczonych dla [Biblioteka programu .NET Framework](/dotnet/framework/index).
 
### <a name="notify-users-of-events-received"></a>Powiadom użytkowników zdarzeń odebranych

[AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) próbki powiadamia użytkowników danych otrzymywanych z czujników lub innych systemów.

### <a name="get-started-with-event-hubs"></a>Rozpoczynanie pracy z usługą Event Hubs 

[Event Hubs wprowadzenie](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) przykładzie przedstawiono podstawowe funkcje usługi Event hubs, takich jak tworzenie Centrum zdarzeń, wysyłania zdarzeń do Centrum zdarzeń i korzystanie ze zdarzeń przy użyciu [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).

### <a name="scale-out-event-processing"></a>Skalowanie przetwarzania zdarzeń 

[Skalowania przetwarzania zdarzeń](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) przykładzie pokazano sposób użycia [hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) do dystrybucji obciążenia zużycia strumienia usługi Event Hubs. Widoczny jest sposób wykonania **EventProcessor** i **EventProcessorFactory** obiekty do zarządzania strumienia zdarzeń. 

###  <a name="pull-data-from-sql-into-an-event-hub"></a>Ściąganie danych z bazy danych SQL do Centrum zdarzeń

[SQL ściąganie danych](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) przykładowych pokazano, jak ściąganie danych z tabeli SQL i wypchnąć go do Centrum zdarzeń do użycia jako dane wejściowe w podrzędnych aplikacji analitycznych.

### <a name="pull-web-data-into-an-event-hub"></a>Ściąganie danych sieci web do Centrum zdarzeń 

[Importuj dane z sieci web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) przykładowych pokazano, jak dane z publicznego źródła danych (na przykład dział transportu podawanie informacji ruchu) i wypchnąć go do Centrum zdarzeń.

## <a name="next-steps"></a>Kolejne kroki

Więcej informacji na temat wersji systemu .NET Framework, przechodząc na stronę następujących łączy:

- [Struktury i cele](/dotnet/articles/standard/frameworks)
- [.NET framework 4.6 i 4.5](/dotnet/framework/index)

Użytkownik może dowiedzieć się więcej o centra zdarzeń w następujących artykułach:

- [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
- [Tworzenie centrum zdarzeń](event-hubs-create.md)
- [Event Hubs — często zadawane pytania](event-hubs-faq.md)