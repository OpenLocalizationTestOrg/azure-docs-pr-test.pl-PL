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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="140e7-103">Jak toouse usługi Service Bus tematów i subskrypcji z języka Python</span><span class="sxs-lookup"><span data-stu-id="140e7-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="140e7-104">W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="140e7-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="140e7-105">Witaj przykłady są napisane w języku Python i używają hello [pakiet Azure Python SDK][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="140e7-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="140e7-106">Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="140e7-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="140e7-107">Aby uzyskać więcej informacji o tematach i subskrypcjach, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="140e7-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="140e7-108">Jeśli potrzebujesz tooinstall Python lub hello [pakiet języka Python Azure][Azure Python package], zobacz hello [Przewodnik instalacji języka Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="140e7-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="140e7-109">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="140e7-109">Create a topic</span></span>
<span data-ttu-id="140e7-110">Witaj **ServiceBusService** obiektu umożliwia toowork z tematów.</span><span class="sxs-lookup"><span data-stu-id="140e7-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="140e7-111">Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="140e7-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="140e7-112">Witaj poniższy kod tworzy **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="140e7-113">Zastąp `mynamespace`, `sharedaccesskeyname`, i `sharedaccesskey` z obszaru nazw rzeczywiste, nazwy i klucza wartość klucza dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="140e7-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="140e7-114">Witaj wartości dla nazwy klucza SAS hello i wartość można uzyskać z hello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="140e7-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="140e7-115">Witaj `create_topic` metoda obsługuje również dodatkowe opcje umożliwiające toooverride domyślny temat ustawienia, takie jak wiadomości godzina temat toolive lub maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="140e7-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="140e7-116">Witaj poniższy przykład ustawia hello tematu maksymalny rozmiar too5 GB i toolive (TTL) wartość czasu wynoszącym 1 minutę:</span><span class="sxs-lookup"><span data-stu-id="140e7-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="140e7-117">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="140e7-117">Create subscriptions</span></span>
<span data-ttu-id="140e7-118">Subskrypcje tootopics również są tworzone za pomocą hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="140e7-119">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.</span><span class="sxs-lookup"><span data-stu-id="140e7-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="140e7-120">Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello toowhich tematu one subskrybowanych, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="140e7-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="140e7-121">Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="140e7-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="140e7-122">Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="140e7-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="140e7-123">Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="140e7-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="140e7-124">Witaj poniższy przykład tworzy subskrypcję o nazwie `AllMessages` i używa hello domyślne **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="140e7-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="140e7-125">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="140e7-125">Create subscriptions with filters</span></span>
<span data-ttu-id="140e7-126">Można także zdefiniować filtry, które pozwalają toospecify wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="140e7-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="140e7-127">Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **SqlFilter**, która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="140e7-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="140e7-128">Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="140e7-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="140e7-129">Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, zobacz hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.</span><span class="sxs-lookup"><span data-stu-id="140e7-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="140e7-130">Filtry tooa subskrypcji można dodać za pomocą hello **utworzyć\_reguły** metody hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="140e7-131">Ta metoda umożliwia tooadd nowe filtry tooan istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="140e7-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="140e7-132">Ponieważ hello domyślnego filtru jest stosowane automatycznie tooall nowych subskrypcji, należy najpierw usunąć hello domyślnego filtru lub hello **MatchAll** zastępują inne filtry, można określić.</span><span class="sxs-lookup"><span data-stu-id="140e7-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="140e7-133">Można usunąć reguły domyślnej hello przy użyciu hello `delete_rule` metody hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="140e7-134">Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `messagenumber` właściwości wyższej niż 3:</span><span class="sxs-lookup"><span data-stu-id="140e7-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="140e7-135">Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z **SqlFilter** który wybiera tylko komunikaty, które mają `messagenumber` właściwości mniejszą lub równą too3:</span><span class="sxs-lookup"><span data-stu-id="140e7-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="140e7-136">Teraz, gdy wiadomość jest wysyłana za`mytopic` zawsze jest dostarczany toohello tooreceivers subskrybowane **AllMessages** subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello **HighMessages**  i **LowMessages** subskrypcje tematu (w zależności od zawartości komunikatu hello).</span><span class="sxs-lookup"><span data-stu-id="140e7-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="140e7-137">Wysyłanie wiadomości tooa tematu</span><span class="sxs-lookup"><span data-stu-id="140e7-137">Send messages tooa topic</span></span>
<span data-ttu-id="140e7-138">toosend tematu usługi Service Bus tooa komunikatu musi używać aplikacja hello `send_topic_message` metody hello **ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="140e7-139">Witaj poniższym przykładzie pokazano, jak komunikaty toosend pięciu testu za`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="140e7-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="140e7-140">Należy pamiętać, że hello `messagenumber` wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (określa subskrypcje, które go otrzymają):</span><span class="sxs-lookup"><span data-stu-id="140e7-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="140e7-141">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="140e7-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="140e7-142">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="140e7-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="140e7-143">Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="140e7-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="140e7-144">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="140e7-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="140e7-145">Aby uzyskać więcej informacji na temat przydziałów, zobacz [przydziały usługi Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="140e7-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="140e7-146">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="140e7-146">Receive messages from a subscription</span></span>
<span data-ttu-id="140e7-147">Komunikaty są odbierane z subskrypcji przy użyciu hello `receive_subscription_message` metody na powitania **ServiceBusService** obiektu:</span><span class="sxs-lookup"><span data-stu-id="140e7-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="140e7-148">Wiadomości są usuwane z subskrypcji hello podczas ich podczas wczytywania hello parametru `peek_lock` ustawiono zbyt**False**.</span><span class="sxs-lookup"><span data-stu-id="140e7-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="140e7-149">Można odczytać (peek) i Zablokuj wiadomość hello bez jego usuwania z kolejki hello przez ustawienie parametru hello `peek_lock` za**True**.</span><span class="sxs-lookup"><span data-stu-id="140e7-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="140e7-150">Witaj zachowanie odczytu i usuwanie wiadomości powitania jako część hello operacji odbierania jest hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="140e7-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="140e7-151">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="140e7-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="140e7-152">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="140e7-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="140e7-153">Jeśli hello `peek_lock` ustawiona jest zbyt**True**, hello odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="140e7-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="140e7-154">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="140e7-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="140e7-155">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `delete` metody na powitania **komunikat** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="140e7-156">Witaj `delete` metoda oznacza hello komunikat jako wykorzystany i usunie go z hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="140e7-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="140e7-157">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="140e7-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="140e7-158">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="140e7-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="140e7-159">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlock` metody na powitania **komunikat** obiektu.</span><span class="sxs-lookup"><span data-stu-id="140e7-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="140e7-160">Spowoduje to spowodować, że wiadomość hello toounlock usługi Service Bus w ramach subskrypcji hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="140e7-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="140e7-161">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji hello i jeśli aplikacja hello nie powiedzie się wiadomość hello tooprocess przed hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), następnie usługi Service Bus umożliwia odblokowanie wiadomość hello automatycznie i ułatwia dostępne toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="140e7-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="140e7-162">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `delete` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="140e7-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="140e7-163">Jest to często nazywane *przetwarzaniem co najmniej raz*, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="140e7-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="140e7-164">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="140e7-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="140e7-165">Jest to często osiągane przy użyciu hello **MessageId** właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="140e7-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="140e7-166">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="140e7-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="140e7-167">Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="140e7-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="140e7-168">Witaj poniższy przykład przedstawia sposób nazywania tematu hello toodelete `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="140e7-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="140e7-169">Usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.</span><span class="sxs-lookup"><span data-stu-id="140e7-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="140e7-170">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="140e7-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="140e7-171">Witaj poniższy kod przedstawia sposób toodelete subskrypcję o nazwie `HighMessages` z hello `mytopic` tematu:</span><span class="sxs-lookup"><span data-stu-id="140e7-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="140e7-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="140e7-172">Next steps</span></span>
<span data-ttu-id="140e7-173">Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="140e7-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="140e7-174">Zobacz [kolejki, tematy i subskrypcje][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="140e7-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="140e7-175">Odwołanie do [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="140e7-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
