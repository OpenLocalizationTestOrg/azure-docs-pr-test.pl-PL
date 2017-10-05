---
title: "Jak używać tematów usługi Service Bus (Ruby) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać tematów usługi Service Bus i subskrypcji platformy Azure. Przykłady kodu są napisane dla aplikacji dopisków fonetycznych."
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
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="2344a-104">Jak używać tematów usługi Service Bus i subskrypcje z Ruby</span><span class="sxs-lookup"><span data-stu-id="2344a-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="2344a-105">W tym artykule opisano, jak używać tematów usługi Service Bus i subskrypcji z aplikacji dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="2344a-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="2344a-106">Omówione scenariusze obejmują **tworzenie tematów i subskrypcji, tworzenie filtrów subskrypcji, wysyłanie komunikatów** do tematu, **odbieranie komunikatów z subskrypcji**, i **usuwanie Tematy i subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="2344a-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="2344a-107">Aby uzyskać więcej informacji dotyczących tematów i subskrypcji, zobacz [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="2344a-108">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="2344a-108">Create a topic</span></span>
<span data-ttu-id="2344a-109">**Azure::ServiceBusService** obiektu umożliwia pracę z tematów.</span><span class="sxs-lookup"><span data-stu-id="2344a-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="2344a-110">Poniższy kod tworzy **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-111">Aby utworzyć temat, użyj `create_topic()` metody.</span><span class="sxs-lookup"><span data-stu-id="2344a-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="2344a-112">Poniższy przykład tworzy temat lub drukuje się błędy, jeśli istnieją.</span><span class="sxs-lookup"><span data-stu-id="2344a-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="2344a-113">Można również przekazać **Azure::ServiceBus::Topic** obiektu dodatkowe opcje, które umożliwiają zastąpienie domyślnych ustawień tematu, takie jak czas wiadomości do kolejki na żywo lub maksymalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="2344a-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="2344a-114">W poniższym przykładzie przedstawiono ustawienie Maksymalny rozmiar kolejki 5 GB i czas wygaśnięcia na 1 minutę:</span><span class="sxs-lookup"><span data-stu-id="2344a-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="2344a-115">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2344a-115">Create subscriptions</span></span>
<span data-ttu-id="2344a-116">Subskrypcje tematu są również tworzone za pomocą **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-117">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów dostarczonych do wirtualnej kolejki subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="2344a-118">Subskrypcje są trwałe i będzie nadal istnieć do czasu albo lub temat są skojarzone z, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="2344a-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="2344a-119">Jeśli Twoja aplikacja logiki, aby utworzyć subskrypcję, jej należy najpierw sprawdź, czy ta subskrypcja już istnieje przy użyciu metody getSubscription.</span><span class="sxs-lookup"><span data-stu-id="2344a-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="2344a-120">Tworzenie subskrypcji z filtrem domyślnym (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="2344a-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="2344a-121">Filtr **MatchAll** jest filtrem domyślnym, który jest używany, gdy podczas tworzenia nowej subskrypcji nie został określony żaden filtr.</span><span class="sxs-lookup"><span data-stu-id="2344a-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="2344a-122">Gdy **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane do tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="2344a-123">Poniższy przykład tworzy subskrypcję o nazwie "all — liczba komunikatów" i używa domyślnej **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="2344a-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="2344a-124">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="2344a-124">Create subscriptions with filters</span></span>
<span data-ttu-id="2344a-125">Można również zdefiniować filtry, które pozwalają określić, które powinny być widoczne wiadomości wysłanych do tematu w ramach określonej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="2344a-126">Najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest **Azure::ServiceBus::SqlFilter**, która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="2344a-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="2344a-127">Filtry SQL działają na właściwościach komunikatów, które są publikowane do tematu.</span><span class="sxs-lookup"><span data-stu-id="2344a-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="2344a-128">Aby uzyskać więcej informacji na temat wyrażeń, które mogą być używane z filtrem SQL, przejrzyj [SqlFilter](service-bus-messaging-sql-filter.md) składni.</span><span class="sxs-lookup"><span data-stu-id="2344a-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="2344a-129">Filtry można dodać do subskrypcji przy użyciu `create_rule()` metody **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-130">Ta metoda umożliwia dodawanie nowych filtrów do istniejącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="2344a-131">Ponieważ domyślnego filtru jest automatycznie stosowana do wszystkich nowych subskrypcji, należy najpierw usunąć domyślny filtr lub **MatchAll** zastępują inne filtry, można określić.</span><span class="sxs-lookup"><span data-stu-id="2344a-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="2344a-132">Należy usunąć domyślną regułę przy użyciu `delete_rule()` metoda **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="2344a-133">Poniższy przykład tworzy subskrypcję o nazwie "Wysoki — liczba komunikatów" z **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają niestandardowy `message_number` właściwości wyższej niż 3:</span><span class="sxs-lookup"><span data-stu-id="2344a-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="2344a-134">Podobnie poniższy przykład tworzy subskrypcję o nazwie `low-messages` z **Azure::ServiceBus::SqlFilter** który wybiera tylko komunikaty, które mają `message_number` właściwości mniej niż 3:</span><span class="sxs-lookup"><span data-stu-id="2344a-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

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

<span data-ttu-id="2344a-135">Teraz wysłania komunikatu do `test-topic`, on zawsze jest dostarczany do odbiorców `all-messages` subskrypcję tematu i selektywnie dostarczany do odbiorców mających subskrypcję `high-messages` i `low-messages` subskrypcje tematu (w zależności od zawartości komunikatu).</span><span class="sxs-lookup"><span data-stu-id="2344a-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="2344a-136">Wysyłanie komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="2344a-136">Send messages to a topic</span></span>
<span data-ttu-id="2344a-137">Aby wysłać komunikat do tematu usługi Service Bus, aplikacja musi używać `send_topic_message()` metoda **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-138">Komunikaty wysyłane do tematów usługi Service Bus są wystąpieniami klasy **Azure::ServiceBus::BrokeredMessage** obiektów.</span><span class="sxs-lookup"><span data-stu-id="2344a-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="2344a-139">**Azure::ServiceBus::BrokeredMessage** obiekty mają zestaw właściwości standardowych (takich jak `label` i `time_to_live`), słownik, który jest używany do przechowywania niestandardowych właściwości specyficzne dla aplikacji oraz treść danych ciągu.</span><span class="sxs-lookup"><span data-stu-id="2344a-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="2344a-140">Aplikacja możne ustawić treść komunikatu przez przekazanie wartości ciągu na `send_topic_message()` — metoda i wszystkie wymagane właściwości standardowych zostaną wypełnione przez wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="2344a-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="2344a-141">W poniższym przykładzie pokazano sposób wysyłania pięciu testowych komunikatów do `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="2344a-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="2344a-142">Należy pamiętać, że `message_number` wartość właściwości niestandardowej każdego komunikatu różni się w iteracji pętli (określa, które subskrypcji odbiera on):</span><span class="sxs-lookup"><span data-stu-id="2344a-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="2344a-143">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="2344a-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="2344a-144">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="2344a-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="2344a-145">Nie ma żadnego limitu liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez temat.</span><span class="sxs-lookup"><span data-stu-id="2344a-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="2344a-146">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="2344a-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="2344a-147">Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2344a-147">Receive messages from a subscription</span></span>
<span data-ttu-id="2344a-148">Komunikaty są odbierane z subskrypcją za pomocą `receive_subscription_message()` metoda **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-149">Domyślnie komunikaty są read(peak) i zablokowany bez usuwania go z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="2344a-150">Może odczytywać i usunąć wiadomości z subskrypcji przez ustawienie `peek_lock` opcji w celu **false**.</span><span class="sxs-lookup"><span data-stu-id="2344a-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="2344a-151">Domyślne zachowanie umożliwia odczytywanie i usuwanie operacją dwuetapową, co umożliwia także do obsługi aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="2344a-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="2344a-152">Gdy usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go w celu uniemożliwienia innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2344a-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="2344a-153">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez wywołanie metody `delete_subscription_message()` — metoda i dostarczający komunikat, który ma zostać usunięty jako parametr.</span><span class="sxs-lookup"><span data-stu-id="2344a-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="2344a-154">`delete_subscription_message()` — Metoda będzie oznaczyć komunikat jako wykorzystany i usunąć go z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2344a-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="2344a-155">Jeśli `:peek_lock` ustawiono parametr **false**, odczytywanie i usuwanie wiadomości staje się najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="2344a-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="2344a-156">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="2344a-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="2344a-157">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="2344a-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="2344a-158">W poniższym przykładzie pokazano, jak mogą być odbierane wiadomości i przetworzone przy użyciu `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="2344a-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="2344a-159">Przykładzie najpierw odbiera i usuwa komunikat z `low-messages` subskrypcji przy użyciu `:peek_lock` ustawioną **false**, a następnie odbierze kolejną wiadomość z `high-messages` , a następnie usunięcie wiadomości za pomocą `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="2344a-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="2344a-160">Sposób obsługi awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="2344a-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="2344a-161">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="2344a-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="2344a-162">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać `unlock_subscription_message()` metoda **Azure::ServiceBusService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2344a-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="2344a-163">Powoduje to odblokowanie komunikatu w subskrypcji przez usługę Service Bus i ponowne udostępnienie go do odebrania przez tę samą lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="2344a-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="2344a-164">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w subskrypcji i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady upływem (na przykład jeśli wystąpiła awaria aplikacji), Usługa Service Bus zostanie automatycznie odblokowanie komunikatu i udostępnienie go do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="2344a-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="2344a-165">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem `delete_subscription_message()` metoda jest wywoływana, a następnie wiadomość jest dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="2344a-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="2344a-166">Jest to często nazywane *przetwarzaniem co najmniej raz*; oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="2344a-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="2344a-167">Jeśli scenariusz nie toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę do swojej aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="2344a-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="2344a-168">Istotą takiej logiki jest często osiągane przy użyciu `message_id` właściwości wiadomości, która pozostaje stała między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="2344a-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="2344a-169">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2344a-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="2344a-170">Tematy i subskrypcje są trwałe i musi zostać jawnie usunięte przez [portalu Azure] [ Azure portal] lub programowo.</span><span class="sxs-lookup"><span data-stu-id="2344a-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="2344a-171">W poniższym przykładzie pokazano sposób usuwania tematu o nazwie `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="2344a-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="2344a-172">Usunięcie tematu powoduje również usunięcie subskrypcji, które są zarejestrowane z tematem.</span><span class="sxs-lookup"><span data-stu-id="2344a-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="2344a-173">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="2344a-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="2344a-174">Poniższy kod ilustruje sposób usuwania subskrypcji o nazwie `high-messages` z `test-topic` tematu:</span><span class="sxs-lookup"><span data-stu-id="2344a-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="2344a-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2344a-175">Next steps</span></span>
<span data-ttu-id="2344a-176">Teraz, kiedy znasz już podstawy tematów usługi Service Bus, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="2344a-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="2344a-177">Zobacz [kolejki, tematy i subskrypcje](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="2344a-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="2344a-178">Dokumentacja interfejsów API dla elementu [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="2344a-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="2344a-179">Odwiedź stronę [zestawu Azure SDK dla środowiska Ruby](https://github.com/Azure/azure-sdk-for-ruby) repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="2344a-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
