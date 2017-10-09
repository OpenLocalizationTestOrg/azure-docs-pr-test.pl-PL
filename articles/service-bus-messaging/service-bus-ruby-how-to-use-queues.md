---
title: kolejkuje toouse aaaHow Azure Service Bus z Ruby | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak kolejki toouse usługi Service Bus na platformie Azure. Przykłady kodu napisane w języku Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Jak kolejki usługi Service Bus toouse z Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

W tym przewodniku opisano sposób toouse kolejek usługi Service Bus. Witaj przykłady są napisane w języku Ruby i używają hello Azure gem. Witaj omówione scenariusze obejmują **tworzenie kolejek, wysyłanie i odbieranie wiadomości**, i **usuwanie kolejek**. Aby uzyskać więcej informacji na temat kolejek usługi Service Bus, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Jak toocreate kolejki
Witaj **Azure::ServiceBusService** obiektu umożliwia toowork z kolejki. toocreate kolejki, użyj hello `create_queue()` metody. Witaj poniższy przykład tworzy kolejkę lub błędy do drukowania.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

Można również przekazać **Azure::ServiceBus::Queue** obiekt dodatkowe opcje, który umożliwia toooverride hello domyślne ustawienia kolejki, takich jak rozmiar kolejki toolive lub maksymalny czas wiadomości. Hello poniższy przykład przedstawia sposób tooset hello kolejki maksymalny rozmiar too5 GB i godzinę, minutę toolive too1:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Jak toosend tooa kolejka komunikatów
toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `send_queue_message()` metody na powitania **Azure::ServiceBusService** obiektu. Komunikaty wysłane za (i odebrane z) usługi Service Bus są kolejki **Azure::ServiceBus::BrokeredMessage** obiekty i mają zestaw właściwości standardowych (takich jak `label` i `time_to_live`), słownik, który jest używany toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji. Aplikację można ustawić hello treści wiadomości powitania przez przekazanie wartości ciągu jako wiadomość hello oraz wszelkie wymagane właściwości standardowe są wypełniane przy użyciu wartości domyślnych.

Witaj poniższym przykładzie pokazano, jak toosend toohello kolejki wiadomości testowej o nazwie `test-queue` przy użyciu `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello. Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB.

## <a name="how-tooreceive-messages-from-a-queue"></a>Jak tooreceive wiadomości z kolejki
Komunikaty są odbierane z kolejki przy użyciu hello `receive_queue_message()` metody na powitania **Azure::ServiceBusService** obiektu. Domyślnie komunikaty są odczytywanie oraz zablokowany bez są usuwane z kolejki hello. Jednak można usunąć wiadomości z kolejki hello podczas wczytywania przez ustawienie hello `:peek_lock` opcję zbyt**false**.

zachowanie domyślne Hello sprawia, że hello odczytywanie i usuwanie operacją dwuetapową, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `delete_queue_message()` — metoda i zapewnianie toobe wiadomość hello usunąć jako parametr. Witaj `delete_queue_message()` — metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z kolejki hello.

Jeśli hello `:peek_lock` ustawiona jest zbyt**false**, odczytywanie i usuwanie wiadomości powitania staje się hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie hello Wystąpił błąd. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ Usługa Service Bus został oznaczony hello komunikat jako wykorzystany, gdy aplikacja hello ponownego uruchomienia i rozpocznie korzystanie z komunikatów ponownie, pominie utracony komunikat hello, który został wykorzystany przed toohello awarii.

Witaj poniższym przykładzie pokazano, jak tooreceive procesu wiadomości i przy użyciu `receive_queue_message()`. przykład Witaj najpierw odbiera i usuwa komunikat przy użyciu `:peek_lock` ustawić także**false**, otrzyma kolejną wiadomość i następnie usuwa hello komunikat przy użyciu `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlock_queue_message()` metody na powitania **Azure::ServiceBusService** obiektu. To powoduje wywołanie usługi Service Bus toounlock hello wiadomości w kolejce hello i stał się dostępny toobe odbioru, albo przez hello sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello i jeśli aplikacja hello nie powiedzie się wiadomość hello tooprocess przed hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), następnie usługi Service Bus umożliwia odblokowanie wiadomość hello automatycznie i ułatwia dostępne toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `delete_queue_message()` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Ten proces jest często nazywany *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat jest przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello `message_id` właściwości wiadomości powitania, która pozostaje stała między kolejnymi próbami dostarczenia.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy kolejek usługi Service Bus hello, wykonaj te więcej toolearn łącza.

* Omówienie [kolejki, tematy i subskrypcje](service-bus-queues-topics-subscriptions.md).
* Odwiedź hello [zestawu Azure SDK dla środowiska Ruby](https://github.com/Azure/azure-sdk-for-ruby) repozytorium w witrynie GitHub.

Porównanie między kolejek usługi Azure Service Bus hello omówione w tym artykule i kolejek Azure opisano w hello [jak toouse magazynu kolejek w języku Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) artykułu, zobacz [kolejek Azure oraz Azure kolejek usługi Service Bus - porównaniu i odróżniające](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

