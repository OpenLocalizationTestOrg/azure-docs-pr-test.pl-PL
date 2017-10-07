---
title: "Tematy dotyczące usługi Azure Service Bus toouse aaaHow języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure Service Bus tematy i subskrypcje w języku Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Jak toouse usługi Service Bus tematów i subskrypcji z języka Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji. Witaj przykłady są napisane w języku Python i używają hello [pakiet Azure Python SDK][Azure Python package]. Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**. Aby uzyskać więcej informacji o tematach i subskrypcjach, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Jeśli potrzebujesz tooinstall Python lub hello [pakiet języka Python Azure][Azure Python package], zobacz hello [Przewodnik instalacji języka Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>Tworzenie tematu
Witaj **ServiceBusService** obiektu umożliwia toowork z tematów. Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do usługi Service Bus:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Witaj poniższy kod tworzy **ServiceBusService** obiektu. Zastąp `mynamespace`, `sharedaccesskeyname`, i `sharedaccesskey` z obszaru nazw rzeczywiste, nazwy i klucza wartość klucza dostępu sygnatury dostępu Współdzielonego.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Witaj wartości dla nazwy klucza SAS hello i wartość można uzyskać z hello [portalu Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Witaj `create_topic` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślny temat ustawienia, takie jak wiadomości godzina temat toolive lub maksymalny rozmiar. Witaj poniższy przykład ustawia hello tematu maksymalny rozmiar too5 GB i toolive (TTL) wartość czasu wynoszącym 1 minutę:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Tworzenie subskrypcji
Subskrypcje tootopics również są tworzone za pomocą hello **ServiceBusService** obiektu. Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.

> [!NOTE]
> Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello toowhich tematu one subskrybowanych, zostaną usunięte.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello
Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji. Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello. Witaj poniższy przykład tworzy subskrypcję o nazwie `AllMessages` i używa hello domyślne **MatchAll** filtru.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Tworzenie subskrypcji z filtrami
Można także zdefiniować filtry, które pozwalają toospecify wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.

Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **SqlFilter**, która implementuje podzbiór standardu SQL92. Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu. Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, zobacz hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.

Filtry tooa subskrypcji można dodać za pomocą hello **utworzyć\_reguły** metody hello **ServiceBusService** obiektu. Ta metoda umożliwia tooadd nowe filtry tooan istniejącej subskrypcji.

> [!NOTE]
> Ponieważ hello domyślnego filtru jest stosowane automatycznie tooall nowych subskrypcji, należy najpierw usunąć hello domyślnego filtru lub hello **MatchAll** zastępują inne filtry, można określić. Można usunąć reguły domyślnej hello przy użyciu hello `delete_rule` metody hello **ServiceBusService** obiektu.
> 
> 

Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `messagenumber` właściwości wyższej niż 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają `messagenumber` właściwości mniejszą lub równą too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Teraz, gdy wiadomość jest wysyłana za`mytopic` zawsze jest dostarczany toohello tooreceivers subskrybowane **AllMessages** subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello **HighMessages**  i **LowMessages** subskrypcje tematu (w zależności od zawartości komunikatu hello).

## <a name="send-messages-tooa-topic"></a>Wysyłanie wiadomości tooa tematu
toosend tematu usługi Service Bus tooa komunikatu musi używać aplikacja hello `send_topic_message` metody hello **ServiceBusService** obiektu.

Witaj poniższym przykładzie pokazano, jak komunikaty toosend pięciu testu za`mytopic`. Należy pamiętać, że hello `messagenumber` wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (określa subskrypcje, które go otrzymają):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello. Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB. Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Odbieranie komunikatów z subskrypcji
Komunikaty są odbierane z subskrypcji przy użyciu hello `receive_subscription_message` metody na powitania **ServiceBusService** obiektu:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

Wiadomości są usuwane z subskrypcji hello podczas ich podczas wczytywania hello parametru `peek_lock` ustawiono zbyt**False**. Można odczytać (peek) i Zablokuj wiadomość hello bez jego usuwania z kolejki hello przez ustawienie parametru hello `peek_lock` za**True**.

Witaj zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

Jeśli hello `peek_lock` ustawiona jest zbyt**True**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `delete` metody na powitania **komunikat** obiektu. Witaj `delete` metoda oznacza hello komunikat jako wykorzystany i usunie go z hello subskrypcji.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlock` metody na powitania **komunikat** obiektu. Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w ramach subskrypcji hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji hello i jeśli aplikacja hello nie powiedzie się wiadomość hello tooprocess przed hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), następnie usługi Service Bus umożliwia odblokowanie wiadomość hello automatycznie i ułatwia dostępne toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `delete` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="delete-topics-and-subscriptions"></a>Usuwanie tematów i subskrypcji
Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo. Witaj poniższy przykład przedstawia sposób nazywania tematu hello toodelete `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu. Subskrypcje mogą być również usuwane niezależnie. Witaj poniższy kod przedstawia sposób toodelete subskrypcję o nazwie `HighMessages` z hello `mytopic` tematu:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.

* Zobacz [kolejki, tematy i subskrypcje][Queues, topics, and subscriptions].
* Odwołanie do [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
