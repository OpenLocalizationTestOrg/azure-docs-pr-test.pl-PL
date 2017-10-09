---
title: "kolejkuje toouse aaaHow Azure Service Bus z języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure Service Bus kolejek w języku Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Jak kolejki usługi Service Bus toouse języka Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

W tym artykule opisano sposób toouse kolejek usługi Service Bus. Witaj przykłady są napisane w języku Python i używają hello [pakiet języka Python Azure Service Bus][Python Azure Service Bus package]. Witaj omówione scenariusze obejmują **tworzenie kolejek, wysyłanie i odbieranie wiadomości**, i **usuwanie kolejek**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python lub hello [pakiet języka Python Azure Service Bus][Python Azure Service Bus package], zobacz hello [Przewodnik instalacji języka Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Tworzenie kolejki
Witaj **ServiceBusService** obiektu umożliwia toowork z kolejki. Dodaj następującego kodu dla dowolnego pliku Python, w którym chcesz tooprogrammatically dostępu do usługi Service Bus górze hello hello:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Witaj poniższy kod tworzy **ServiceBusService** obiektu. Zastąp `mynamespace`, `sharedaccesskeyname`, i `sharedaccesskey` nazwą przestrzeni nazw, nazwę klucza sygnatury dostępu Współdzielonego dostępu współdzielonego i wartość.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello wartości nazwy klucza SAS hello i wartości można znaleźć w hello [portalu Azure] [ Azure portal] informacje dotyczące połączenia, lub w Visual Studio hello **właściwości** okienku, wybierając Witaj przestrzeń nazw magistrali usług w Eksploratorze serwera (jak pokazano w poprzedniej sekcji hello).

```python
bus_service.create_queue('taskqueue')
```

Witaj `create_queue` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślne kolejki ustawienia, takie jak toolive czasu wiadomości (TTL) lub maksymalny rozmiar kolejki. Witaj poniższy przykład ustawia hello kolejki maksymalny rozmiar too5 GB i minutę too1 wartość TTL hello:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Komunikaty tooa kolejki wysyłania
toosend kolejki usługi Service Bus tooa wiadomość hello wywołuje aplikacji `send_queue_message` metody na powitania **ServiceBusService** obiektu.

Witaj poniższym przykładzie pokazano, jak toosend toohello kolejki wiadomości testowej o nazwie `taskqueue` przy użyciu `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Kolejki usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu liczby hello wiadomości w kolejce, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez kolejkę wiadomości powitania hello. Ten rozmiar kolejki jest definiowany w czasie tworzenia, z górnym limitem 5 GB. Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Odbieranie komunikatów z kolejki
Komunikaty są odbierane z kolejki przy użyciu hello `receive_queue_message` metody na powitania **ServiceBusService** obiektu:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

Wiadomości są usuwane z kolejki hello podczas ich podczas wczytywania hello parametru `peek_lock` ustawiono zbyt**False**. Można odczytać (peek) i Zablokuj wiadomość hello bez jego usuwania z kolejki hello przez ustawienie parametru hello `peek_lock` za**True**.

Witaj zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

Jeśli hello `peek_lock` ustawiona jest zbyt**True**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie hello procesu **usunąć** metody na powitania **komunikat** obiektu. Witaj **usunąć** — metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z kolejki hello.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **odblokować** metody na powitania **komunikat** obiektu. Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w kolejce hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w kolejce hello, a jeśli hello hello aplikacji kończy się niepowodzeniem, które tooprocess hello komunikatu przed przekroczenie limitu czasu blokady upływem (np. Jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **usunąć** metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz następujące artykuły toolearn więcej.

* [Kolejki, tematy i subskrypcje][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

