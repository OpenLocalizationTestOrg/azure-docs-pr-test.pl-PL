---
title: "Jak używać tematów usługi Azure Service Bus z językiem Java | Dokumentacja firmy Microsoft"
description: "Używać tematów usługi Service Bus i subskrypcji platformy Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="1cd1b-103">Jak używać tematów usługi Service Bus i subskrypcje z językiem Java</span><span class="sxs-lookup"><span data-stu-id="1cd1b-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="1cd1b-104">W tym przewodniku opisano, jak używać tematów usługi Service Bus i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="1cd1b-105">Przykłady są napisane w języku Java i użyj [zestawu Azure SDK dla języka Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="1cd1b-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="1cd1b-106">Omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłanie komunikatów do tematu**, **odbieranie komunikatów z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="1cd1b-107">Co to są tematy i subskrypcje usługi Service Bus?</span><span class="sxs-lookup"><span data-stu-id="1cd1b-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="1cd1b-108">Tematy i subskrypcje usługi Service Bus obsługują model komunikacji z użyciem *publikowania/subskrypcji* komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="1cd1b-109">Podczas korzystania z tematów i subskrypcji składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem tematu, która działa jako pośrednik.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="1cd1b-111">W przeciwieństwie do kolejek usługi Service Bus, w których każdy komunikat jest przetwarzany przez jednego konsumenta, tematy i subskrypcje zapewniają formę komunikacji „jeden do wielu” z użyciem wzorca publikowania/subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="1cd1b-112">Istnieje możliwość zarejestrowania wielu subskrypcji danego tematu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="1cd1b-113">Po wysłaniu komunikatu do tematu jest on następnie udostępniany poszczególnym subskrypcjom w celu niezależnej obsługi lub niezależnego przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="1cd1b-114">Subskrypcja tematu przypomina wirtualną kolejkę, która odbiera kopie komunikatów wysłanych do tematu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="1cd1b-115">Opcjonalnie można zarejestrować reguły filtrów dla tematu oparte na subskrypcji, co pozwala na filtru/ograniczanie komunikatów do tematu są odbierane przez poszczególne subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="1cd1b-116">Tematy usługi Service Bus i subskrypcje umożliwiają skalowanie przetwarzania bardzo dużej liczby komunikatów w bardzo dużej liczby użytkowników i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="1cd1b-117">Tworzenie przestrzeni nazw usługi</span><span class="sxs-lookup"><span data-stu-id="1cd1b-117">Create a service namespace</span></span>
<span data-ttu-id="1cd1b-118">Aby rozpocząć korzystanie z usługi Service Bus tematów i subskrypcji platformy Azure, należy najpierw utworzyć przestrzeń nazw zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="1cd1b-119">Aby utworzyć przestrzeń nazw:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="1cd1b-120">Skonfigurować aplikację do użycia z magistralą usług</span><span class="sxs-lookup"><span data-stu-id="1cd1b-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="1cd1b-121">Upewnij się, że zainstalowano [zestawu Azure SDK dla języka Java] [ Azure SDK for Java] przed zbudowaniem tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="1cd1b-122">Jeśli używasz programu Eclipse, możesz zainstalować [zestawu narzędzi platformy Azure dla programu Eclipse] [ Azure Toolkit for Eclipse] zawierającą zestaw Azure SDK dla języka Java.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="1cd1b-123">Następnie można dodać **bibliotek usługi Microsoft Azure dla języka Java** do projektu:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="1cd1b-124">Dodaj następujące `import` instrukcje na początku pliku Java:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="1cd1b-125">Dodaj biblioteki Azure dla języka Java do ścieżki kompilacji i uwzględnić go w tym zestawem wdrażania projektu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="1cd1b-126">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="1cd1b-126">Create a topic</span></span>
<span data-ttu-id="1cd1b-127">Operacje zarządzania dla tematów usługi Service Bus można wykonywać za pomocą **ServiceBusContract** klasy.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="1cd1b-128">A **ServiceBusContract** obiekt jest tworzony z odpowiednią konfiguracją, która hermetyzuje tokenu sygnatury dostępu Współdzielonego z uprawnieniami do zarządzania nim, oraz **ServiceBusContract** klasy jest jedynym punktem komunikacji z usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="1cd1b-129">**ServiceBusService** klasa dostarcza metody do tworzenia, wyliczania i usuwania tematów.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="1cd1b-130">W poniższym przykładzie przedstawiono sposób **ServiceBusService** obiekt może służyć do utworzenia tematu o nazwie `TestTopic`, przestrzeń nazw o nazwie `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="1cd1b-131">Brak metody na **TopicInfo** umożliwiających właściwości tematu, należy ustawić wartość (na przykład: odpowiada wartości domyślne time to live (TTL) do zastosowania dla komunikatów wysyłanych do tematu).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="1cd1b-132">Poniższy przykład pokazuje, jak utworzyć temat o nazwie `TestTopic` o maksymalnym rozmiarze 5 GB:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="1cd1b-133">Należy pamiętać, że można użyć **listTopics** metoda **ServiceBusContract** obiektów, aby sprawdzić, czy temat o określonej nazwie już istnieje w przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="1cd1b-134">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1cd1b-134">Create subscriptions</span></span>
<span data-ttu-id="1cd1b-135">Subskrypcje do tematów, również są tworzone za pomocą **ServiceBusService** klasy.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="1cd1b-136">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="1cd1b-137">Tworzenie subskrypcji z filtrem domyślnym (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="1cd1b-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="1cd1b-138">Filtr **MatchAll** jest filtrem domyślnym, który jest używany, gdy podczas tworzenia nowej subskrypcji nie został określony żaden filtr.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="1cd1b-139">Gdy **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane do tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="1cd1b-140">Poniższy przykład tworzy subskrypcję o nazwie „AllMessages” i używa domyślnego filtru **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="1cd1b-141">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="1cd1b-141">Create subscriptions with filters</span></span>
<span data-ttu-id="1cd1b-142">Istnieje również możliwość utworzenia filtrów, które umożliwiają należy do zakresu, które powinny być widoczne wiadomości wysłanych do tematu w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="1cd1b-143">Najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest [SqlFilter][SqlFilter], która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="1cd1b-144">Filtry SQL działają na właściwościach komunikatów, które są publikowane do tematu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="1cd1b-145">Aby uzyskać więcej informacji na temat wyrażeń, które mogą być używane z filtrem SQL, przejrzyj [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="1cd1b-146">Poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają niestandardowy **MessageNumber** Właściwość jest większy niż 3:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="1cd1b-147">Podobnie poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają **MessageNumber** Właściwość mniej niż 3:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="1cd1b-148">Teraz wysłania komunikatu do `TestTopic`, zawsze zostanie dostarczona do odbiorców `AllMessages` subskrypcji i selektywnie dostarczany do odbiorców mających subskrypcję `HighMessages` i `LowMessages` subskrypcji (w zależności od zawartość komunikatu).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="1cd1b-149">Wysyłanie komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="1cd1b-149">Send messages to a topic</span></span>
<span data-ttu-id="1cd1b-150">Aby wysłać komunikat do tematu usługi Service Bus, aplikacja uzyskuje **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="1cd1b-151">Poniższy kod przedstawia sposób wysłania komunikatu `TestTopic` utworzone wcześniej w temacie `HowToSample` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="1cd1b-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="1cd1b-152">Komunikaty wysyłane do tematów usługi Service Bus są wystąpieniami klasy [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="1cd1b-153">[BrokeredMessage][BrokeredMessage]* obiekty mają zestaw metod standardowych (takich jak **setLabel** i **TimeToLive**), słownik, który służy do przechowywania niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="1cd1b-154">Aplikacja możne ustawić treść komunikatu przez przekazanie dowolnego obiektu podlegającego serializacji do konstruktora [BrokeredMessage][BrokeredMessage], a odpowiedni **DataContractSerializer** zostanie następnie użyte do serializacji obiektu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="1cd1b-155">Alternatywnie **java.io.InputStream** można podać.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="1cd1b-156">W poniższym przykładzie pokazano sposób wysyłania pięciu testowych komunikatów do `TestTopic` **MessageSender** możemy uzyskać we fragmencie kodu powyżej.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="1cd1b-157">Uwaga jak **MessageNumber** wartość właściwości każdego komunikatu różni się w iteracji pętli (umożliwi to określenie subskrypcje, które go otrzymają):</span><span class="sxs-lookup"><span data-stu-id="1cd1b-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="1cd1b-158">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w [warstwie Standardowa](service-bus-premium-messaging.md) i 1 MB w [warstwie Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1cd1b-159">Nagłówek, który zawiera standardowe i niestandardowe właściwości aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1cd1b-160">Nie ma żadnego limitu liczby komunikatów w tematu, ale jest ograniczenie całkowitego rozmiaru komunikatów przechowywanych przez temat.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="1cd1b-161">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="1cd1b-162">Jak odbierać komunikaty z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1cd1b-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="1cd1b-163">Aby odbierać komunikaty z subskrypcji, należy użyć **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="1cd1b-164">Odebrane komunikaty mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="1cd1b-165">Korzystając z **ReceiveAndDelete** trybie odbieranie jest operacją pojedynczego zrzutu - oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu, oznacza komunikat jako wykorzystany i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="1cd1b-166">Tryb **ReceiveAndDelete** jest najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="1cd1b-167">Aby to zrozumieć, rozważmy scenariusz, w którym konsument wystawia żądanie odbioru, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="1cd1b-168">Ponieważ Usługa Service Bus zostanie oznaczona komunikat jako wykorzystany, a następnie po uruchomieniu i rozpocznie korzystanie z komunikatów ponownie aplikacji, pominie utracony komunikat, który został wykorzystany przed awarią.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="1cd1b-169">W **PeekLock** trybie odbieranie staje się operacją dwuetapowy, co umożliwia obsługę aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1cd1b-170">Gdy usługa Service Bus odbiera żądanie, znajduje następny komunikat do wykorzystania, blokuje go w celu uniemożliwienia innym klientom odebrania go i zwraca go do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="1cd1b-171">Kiedy aplikacja zakończy przetwarzanie komunikatu (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap procesu odbierania przez wywołanie metody **usunąć** na odebranym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="1cd1b-172">Kiedy Usługa Service Bus widzi **usunąć** wywołania spowoduje oznaczenie komunikat jako wykorzystany i usunąć go z tematu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="1cd1b-173">Na poniższym przykładzie przedstawiono, jak mogą być odbierane wiadomości i przetworzone przy użyciu **PeekLock** mode (nie tryb domyślny).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="1cd1b-174">W poniższym przykładzie wykonuje pętlę i przetwarza wiadomości w subskrypcji "HighMessages", a następnie kończy działanie, gdy nie ma żadnych komunikatów więcej (możesz też go można można ustawić czekać na nowe komunikaty).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1cd1b-175">Sposób obsługi awarii aplikacji i komunikatów niemożliwych do odczytania</span><span class="sxs-lookup"><span data-stu-id="1cd1b-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="1cd1b-176">Usługa Service Bus zapewnia funkcję ułatwiającą bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1cd1b-177">Jeśli aplikacja odbiorcy nie może przetworzyć komunikatu z jakiegoś powodu, wówczas może wywołać **unlockMessage** metody dla odebranego komunikatu (zamiast **deleteMessage** metody).</span><span class="sxs-lookup"><span data-stu-id="1cd1b-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="1cd1b-178">Spowoduje to odblokowanie komunikatu w temacie i udostępnienie go do ponownego odbioru, przez tę samą lub inną odbierającą aplikację usługę Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1cd1b-179">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w temacie i jeśli aplikacja nie może przetworzyć komunikatu przed przekroczenie limitu czasu blokady wygaśnięcia (na przykład jeśli wystąpiła awaria aplikacji), Usługa Service Bus zostanie automatycznie odblokowanie komunikatu i stał się dostępny do ponownego odbioru.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="1cd1b-180">W przypadku, gdy aplikacja przestaje działać po przetworzeniu komunikatu, ale przed wysłaniem **deleteMessage** żądania, a następnie komunikat zostanie dostarczony do aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="1cd1b-181">Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w pewnych sytuacjach ten sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="1cd1b-182">Jeśli scenariusz nie toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę do swojej aplikacji w celu obsługi dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="1cd1b-183">Jest to często osiągane przy użyciu **getMessageId** — metoda, która pozostaje niezmienna między kolejnymi próbami dostarczenia komunikatu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="1cd1b-184">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1cd1b-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="1cd1b-185">Usuwanie tematów i subskrypcji podstawową metodą jest użycie **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="1cd1b-186">Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane z tematem.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="1cd1b-187">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="1cd1b-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cd1b-188">Next Steps</span></span>
<span data-ttu-id="1cd1b-189">Teraz, kiedy znasz już podstawy kolejek usługi Service Bus, zobacz [kolejek usługi Service Bus, tematy i subskrypcje] [ Service Bus queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1cd1b-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
