---
title: "Tematy usługi Service Bus toouse aaaHow (Ruby) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Service Bus tematów i subskrypcji platformy Azure. Przykłady kodu są napisane dla aplikacji dopisków fonetycznych."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Jak toouse usługi Service Bus tematów i subskrypcji z Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji z aplikacji dopisków fonetycznych. Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji, tworzenie filtrów subskrypcji, wysyłanie komunikatów** tematu tooa **odbieranie komunikatów z subskrypcji**, i  **usuwanie tematów i subskrypcji**. Aby uzyskać więcej informacji na tematy i subskrypcje, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Tworzenie tematu
Witaj **Azure::ServiceBusService** obiektu umożliwia toowork z tematów. Witaj poniższy kod tworzy **Azure::ServiceBusService** obiektu. toocreate tematu, użyj hello `create_topic()` metody. Witaj poniższy przykład tworzy temat lub drukuje hello błędy, jeśli istnieją.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Można również przekazać **Azure::ServiceBus::Topic** obiektu z dodatkowymi opcjami, umożliwiające toooverride domyślny temat ustawienia, takie jak rozmiar kolejki toolive lub maksymalny czas wiadomości. Hello przedstawiono w następującym przykładzie ustawienie hello kolejki maksymalny rozmiar too5 GB i godziny minutę toolive too1:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Tworzenie subskrypcji
Subskrypcje tematu są również tworzone za pomocą hello **Azure::ServiceBusService** obiektu. Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.

Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello tematu one są skojarzone z, zostaną usunięte. Jeśli aplikacja zawiera logikę toocreate subskrypcję, jej należy najpierw sprawdź, czy hello subskrypcji już istnieje przy użyciu metody getSubscription hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello
Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji. Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello. Witaj poniższy przykład tworzy subskrypcję o nazwie "all — liczba komunikatów" i używa hello domyślne **MatchAll** filtru.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Tworzenie subskrypcji z filtrami
Można także zdefiniować filtry, które pozwalają toospecify wysłane wiadomości, które powinny być widoczne tooa tematu w ramach określonej subskrypcji.

Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest hello **Azure::ServiceBus::SqlFilter**, która implementuje podzbiór standardu SQL92. Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu. Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter](service-bus-messaging-sql-filter.md) składni.

Filtry tooa subskrypcji można dodać za pomocą hello `create_rule()` metody hello **Azure::ServiceBusService** obiektu. Ta metoda umożliwia tooadd nowe filtry tooan istniejącej subskrypcji.

Ponieważ hello domyślnego filtru jest stosowana automatycznie tooall nowych subskrypcji, musisz najpierw usunąć hello domyślnego filtru lub hello **MatchAll** zastępują inne filtry, można określić. Można usunąć reguły domyślnej hello przy użyciu hello `delete_rule()` metody na powitania **Azure::ServiceBusService** obiektu.

Witaj poniższy przykład tworzy subskrypcję o nazwie "Wysoki — liczba komunikatów" **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `message_number` właściwości wyższej niż 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `low-messages` z **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają `message_number` właściwości mniejszą lub równą too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Kiedy wiadomość jest teraz wysyłane za`test-topic`, jest zawsze być dostarczonego tooreceivers subskrybowane toohello `all-messages` subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello `high-messages` i `low-messages` (subskrypcje tematu w zależności od zawartości wiadomość hello).

## <a name="send-messages-tooa-topic"></a>Wysyłanie wiadomości tooa tematu
toosend tematu usługi Service Bus tooa komunikatu musi używać aplikacja hello `send_topic_message()` metody na powitania **Azure::ServiceBusService** obiektu. Komunikaty wysyłane są tematy magistrali tooService wystąpień hello **Azure::ServiceBus::BrokeredMessage** obiektów. **Azure::ServiceBus::BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `label` i `time_to_live`), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść danych ciągu. Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie toohello wartość ciągu `send_topic_message()` — metoda i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.

Witaj poniższym przykładzie pokazano, jak komunikaty toosend pięciu testu za`test-topic`. Należy pamiętać, że hello `message_number` wartość właściwości niestandardowej każdego komunikatu różni się na powitania iteracji pętli hello (określa, które subskrypcji odbiera on):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello. Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
Komunikaty są odbierane z subskrypcji przy użyciu hello `receive_subscription_message()` metody na powitania **Azure::ServiceBusService** obiektu. Domyślnie komunikaty są read(peak) i zablokowany bez usuwania go z hello subskrypcji. Może odczytywać i usunąć wiadomość hello z subskrypcji hello przez ustawienie hello `peek_lock` opcję zbyt**false**.

zachowanie domyślne Hello sprawia, że hello odczytywanie i usuwanie operacją dwuetapową, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `delete_subscription_message()` — metoda i zapewnianie toobe wiadomość hello usunąć jako parametr. Witaj `delete_subscription_message()` metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z hello subskrypcji.

Jeśli hello `:peek_lock` ustawiona jest zbyt**false**, odczytywanie i usuwanie wiadomości powitania staje się hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie hello Wystąpił błąd. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receive_subscription_message()`. przykład Witaj najpierw odbiera i usuwa komunikat z hello `low-messages` subskrypcji przy użyciu `:peek_lock` ustawić także**false**, a następnie odbierze kolejną wiadomość z hello `high-messages` , a następnie usuwa hello komunikat przy użyciu `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlock_subscription_message()` metody na powitania **Azure::ServiceBusService** obiektu. Ta powoduje, że usługi Service Bus toounlock hello wiadomości w ramach subskrypcji hello i stał się dostępny toobe odbioru, albo przez hello sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `delete_subscription_message()` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Istotą takiej logiki jest często osiągane przy użyciu hello `message_id` właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="delete-topics-and-subscriptions"></a>Usuwanie tematów i subskrypcji
Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo. Hello w poniższym przykładzie pokazano, jak toodelete hello temat o nazwie `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu. Subskrypcje mogą być również usuwane niezależnie. Witaj poniższy kod przedstawia sposób nazywania subskrypcji hello toodelete `high-messages` z hello `test-topic` tematu:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.

* Zobacz [kolejki, tematy i subskrypcje](service-bus-queues-topics-subscriptions.md).
* Dokumentacja interfejsów API dla elementu [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Odwiedź hello [zestawu Azure SDK dla środowiska Ruby](https://github.com/Azure/azure-sdk-for-ruby) repozytorium w witrynie GitHub.

[Azure portal]: https://portal.azure.com
