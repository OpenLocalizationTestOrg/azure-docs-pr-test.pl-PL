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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="7a6f0-104">Jak toouse usługi Service Bus tematów i subskrypcji z Ruby</span><span class="sxs-lookup"><span data-stu-id="7a6f0-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7a6f0-105">W tym artykule opisano sposób toouse usługi Service Bus tematów i subskrypcji z aplikacji dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="7a6f0-106">Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji, tworzenie filtrów subskrypcji, wysyłanie komunikatów** tematu tooa **odbieranie komunikatów z subskrypcji**, i  **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="7a6f0-107">Aby uzyskać więcej informacji na tematy i subskrypcje, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="7a6f0-108">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="7a6f0-108">Create a topic</span></span>
<span data-ttu-id="7a6f0-109">Witaj **Azure::ServiceBusService** obiektu umożliwia toowork z tematów.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="7a6f0-110">Witaj poniższy kod tworzy **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-111">toocreate tematu, użyj hello `create_topic()` metody.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="7a6f0-112">Witaj poniższy przykład tworzy temat lub drukuje hello błędy, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="7a6f0-113">Można również przekazać **Azure::ServiceBus::Topic** obiektu z dodatkowymi opcjami, umożliwiające toooverride domyślny temat ustawienia, takie jak rozmiar kolejki toolive lub maksymalny czas wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="7a6f0-114">Hello przedstawiono w następującym przykładzie ustawienie hello kolejki maksymalny rozmiar too5 GB i godziny minutę toolive too1:</span><span class="sxs-lookup"><span data-stu-id="7a6f0-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="7a6f0-115">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7a6f0-115">Create subscriptions</span></span>
<span data-ttu-id="7a6f0-116">Subskrypcje tematu są również tworzone za pomocą hello **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-117">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych wirtualnej kolejki subskrypcji toohello hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="7a6f0-118">Subskrypcje są trwałe i będzie kontynuować tooexist dopiero albo lub hello tematu one są skojarzone z, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="7a6f0-119">Jeśli aplikacja zawiera logikę toocreate subskrypcję, jej należy najpierw sprawdź, czy hello subskrypcji już istnieje przy użyciu metody getSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="7a6f0-120">Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="7a6f0-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="7a6f0-121">Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7a6f0-122">Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="7a6f0-123">Witaj poniższy przykład tworzy subskrypcję o nazwie "all — liczba komunikatów" i używa hello domyślne **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7a6f0-124">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="7a6f0-124">Create subscriptions with filters</span></span>
<span data-ttu-id="7a6f0-125">Można także zdefiniować filtry, które pozwalają toospecify wysłane wiadomości, które powinny być widoczne tooa tematu w ramach określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="7a6f0-126">Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest hello **Azure::ServiceBus::SqlFilter**, która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="7a6f0-127">Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="7a6f0-128">Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter](service-bus-messaging-sql-filter.md) składni.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="7a6f0-129">Filtry tooa subskrypcji można dodać za pomocą hello `create_rule()` metody hello **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-130">Ta metoda umożliwia tooadd nowe filtry tooan istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="7a6f0-131">Ponieważ hello domyślnego filtru jest stosowana automatycznie tooall nowych subskrypcji, musisz najpierw usunąć hello domyślnego filtru lub hello **MatchAll** zastępują inne filtry, można określić.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="7a6f0-132">Można usunąć reguły domyślnej hello przy użyciu hello `delete_rule()` metody na powitania **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="7a6f0-133">Witaj poniższy przykład tworzy subskrypcję o nazwie "Wysoki — liczba komunikatów" **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `message_number` właściwości wyższej niż 3:</span><span class="sxs-lookup"><span data-stu-id="7a6f0-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="7a6f0-134">Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `low-messages` z **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają `message_number` właściwości mniejszą lub równą too3:</span><span class="sxs-lookup"><span data-stu-id="7a6f0-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="7a6f0-135">Kiedy wiadomość jest teraz wysyłane za`test-topic`, jest zawsze być dostarczonego tooreceivers subskrybowane toohello `all-messages` subskrypcję tematu i selektywnie dostarczany tooreceivers subskrybowane toohello `high-messages` i `low-messages` (subskrypcje tematu w zależności od zawartości wiadomość hello).</span><span class="sxs-lookup"><span data-stu-id="7a6f0-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="7a6f0-136">Wysyłanie wiadomości tooa tematu</span><span class="sxs-lookup"><span data-stu-id="7a6f0-136">Send messages tooa topic</span></span>
<span data-ttu-id="7a6f0-137">toosend tematu usługi Service Bus tooa komunikatu musi używać aplikacja hello `send_topic_message()` metody na powitania **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-138">Komunikaty wysyłane są tematy magistrali tooService wystąpień hello **Azure::ServiceBus::BrokeredMessage** obiektów.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="7a6f0-139">**Azure::ServiceBus::BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `label` i `time_to_live`), słownik, który jest używane toohold niestandardowe właściwości specyficzne dla aplikacji oraz treść danych ciągu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="7a6f0-140">Aplikacja może ustawić hello treści wiadomości powitania przez przekazanie toohello wartość ciągu `send_topic_message()` — metoda i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="7a6f0-141">Witaj poniższym przykładzie pokazano, jak komunikaty toosend pięciu testu za`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="7a6f0-142">Należy pamiętać, że hello `message_number` wartość właściwości niestandardowej każdego komunikatu różni się na powitania iteracji pętli hello (określa, które subskrypcji odbiera on):</span><span class="sxs-lookup"><span data-stu-id="7a6f0-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="7a6f0-143">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="7a6f0-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7a6f0-144">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7a6f0-145">Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="7a6f0-146">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="7a6f0-147">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7a6f0-147">Receive messages from a subscription</span></span>
<span data-ttu-id="7a6f0-148">Komunikaty są odbierane z subskrypcji przy użyciu hello `receive_subscription_message()` metody na powitania **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-149">Domyślnie komunikaty są read(peak) i zablokowany bez usuwania go z hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="7a6f0-150">Może odczytywać i usunąć wiadomość hello z subskrypcji hello przez ustawienie hello `peek_lock` opcję zbyt**false**.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="7a6f0-151">zachowanie domyślne Hello sprawia, że hello odczytywanie i usuwanie operacją dwuetapową, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7a6f0-152">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="7a6f0-153">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu `delete_subscription_message()` — metoda i zapewnianie toobe wiadomość hello usunąć jako parametr.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="7a6f0-154">Witaj `delete_subscription_message()` metoda będzie oznaczyć hello komunikat jako wykorzystany i usunąć go z hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="7a6f0-155">Jeśli hello `:peek_lock` ustawiona jest zbyt**false**, odczytywanie i usuwanie wiadomości powitania staje się hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie hello Wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="7a6f0-156">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="7a6f0-157">Ponieważ usługi Service Bus będzie zostały oznaczone hello komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="7a6f0-158">Witaj poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="7a6f0-159">przykład Witaj najpierw odbiera i usuwa komunikat z hello `low-messages` subskrypcji przy użyciu `:peek_lock` ustawić także**false**, a następnie odbierze kolejną wiadomość z hello `high-messages` , a następnie usuwa hello komunikat przy użyciu `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="7a6f0-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7a6f0-160">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="7a6f0-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="7a6f0-161">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7a6f0-162">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello `unlock_subscription_message()` metody na powitania **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="7a6f0-163">Ta powoduje, że usługi Service Bus toounlock hello wiadomości w ramach subskrypcji hello i stał się dostępny toobe odbioru, albo przez hello sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7a6f0-164">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji hello, a jeśli wiadomość hello tooprocess przed awarii aplikacji hello hello blokady upłynięciem limitu czasu (na przykład jeśli wystąpiła awaria aplikacji hello), a następnie usługi Service Bus odblokowaniem wiadomość hello automatycznie i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="7a6f0-165">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello `delete_subscription_message()` metoda jest wywoływana, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="7a6f0-166">Jest to często nazywane *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="7a6f0-167">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="7a6f0-168">Istotą takiej logiki jest często osiągane przy użyciu hello `message_id` właściwości wiadomości powitania, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7a6f0-169">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7a6f0-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="7a6f0-170">Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte za pośrednictwem hello [portalu Azure] [ Azure portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="7a6f0-171">Hello w poniższym przykładzie pokazano, jak toodelete hello temat o nazwie `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="7a6f0-172">Usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="7a6f0-173">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="7a6f0-174">Witaj poniższy kod przedstawia sposób nazywania subskrypcji hello toodelete `high-messages` z hello `test-topic` tematu:</span><span class="sxs-lookup"><span data-stu-id="7a6f0-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="7a6f0-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a6f0-175">Next steps</span></span>
<span data-ttu-id="7a6f0-176">Teraz, kiedy znasz już podstawy tematów usługi Service Bus hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="7a6f0-177">Zobacz [kolejki, tematy i subskrypcje](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="7a6f0-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="7a6f0-178">Dokumentacja interfejsów API dla elementu [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="7a6f0-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="7a6f0-179">Odwiedź hello [zestawu Azure SDK dla środowiska Ruby](https://github.com/Azure/azure-sdk-for-ruby) repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a6f0-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
