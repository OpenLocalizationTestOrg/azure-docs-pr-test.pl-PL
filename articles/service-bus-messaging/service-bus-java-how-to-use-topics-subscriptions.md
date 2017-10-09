---
title: "Tematy dotyczące usługi Azure Service Bus toouse aaaHow z językiem Java | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="eb1ed-103">Jak toouse usługi Service Bus tematów i subskrypcji z językiem Java</span><span class="sxs-lookup"><span data-stu-id="eb1ed-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="eb1ed-104">W tym przewodniku opisano sposób toouse usługi Service Bus tematów i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="eb1ed-105">Hello przykłady są napisane w języku Java i używają hello [zestawu Azure SDK dla języka Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="eb1ed-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="eb1ed-106">Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="eb1ed-107">Co to są tematy i subskrypcje usługi Service Bus?</span><span class="sxs-lookup"><span data-stu-id="eb1ed-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="eb1ed-108">Tematy i subskrypcje usługi Service Bus obsługują model komunikacji z użyciem *publikowania/subskrypcji* komunikatów.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="eb1ed-109">Podczas korzystania z tematów i subskrypcji składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem tematu, która działa jako pośrednik.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="eb1ed-111">W przeciwieństwie do kolejek usługi Service Bus, w których każdy komunikat jest przetwarzany przez jednego konsumenta, tematy i subskrypcje zapewniają formę komunikacji „jeden do wielu” z użyciem wzorca publikowania/subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="eb1ed-112">Istnieje możliwość zarejestrowania wielu subskrypcji tooa tematu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="eb1ed-113">Jeżeli tooa tematu jest wysyłany komunikat, jest następnie on proces toohandle subskrypcji tooeach dostępne niezależnie.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="eb1ed-114">Temat tooa subskrypcji przypomina wirtualną kolejkę, która odbiera kopie wiadomości powitania, które zostały wysłane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="eb1ed-115">Opcjonalnie można zarejestrować reguły filtrów dla tematu oparte na subskrypcji, dzięki czemu można toofilter/ograniczyć które tematu tooa komunikaty są odbierane przez poszczególne subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="eb1ed-116">Tematy usługi Service Bus i subskrypcje pozwalają tooprocess tooscale bardzo dużej liczby komunikatów w bardzo dużej liczby użytkowników i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="eb1ed-117">Tworzenie przestrzeni nazw usługi</span><span class="sxs-lookup"><span data-stu-id="eb1ed-117">Create a service namespace</span></span>
<span data-ttu-id="eb1ed-118">toobegin przy użyciu usługi Service Bus tematów i subskrypcji platformy Azure, musisz najpierw utworzyć przestrzeń nazw zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="eb1ed-119">toocreate przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="eb1ed-120">Konfigurowanie sieci toouse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="eb1ed-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="eb1ed-121">Upewnij się, że zainstalowano hello [zestawu Azure SDK dla języka Java] [ Azure SDK for Java] przed zbudowaniem tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="eb1ed-122">Jeśli używasz programu Eclipse, można zainstalować hello [zestawu narzędzi platformy Azure dla programu Eclipse] [ Azure Toolkit for Eclipse] zawierającą hello Azure SDK dla języka Java.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="eb1ed-123">Następnie można dodać hello **bibliotek usługi Microsoft Azure dla języka Java** tooyour projektu:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="eb1ed-124">Dodaj następujące hello `import` toohello instrukcje na początku pliku Java hello:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="eb1ed-125">Dodaj hello biblioteki Azure dla języka Java tooyour zbudować ścieżki i uwzględnić go w tym zestawem wdrażania projektu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="eb1ed-126">Tworzenie tematu</span><span class="sxs-lookup"><span data-stu-id="eb1ed-126">Create a topic</span></span>
<span data-ttu-id="eb1ed-127">Operacje zarządzania dla tematów usługi Service Bus można wykonywać za pomocą **ServiceBusContract** klasy.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="eb1ed-128">A **ServiceBusContract** obiekt jest tworzony z odpowiednią konfiguracją, która hermetyzuje tokenu sygnatury dostępu Współdzielonego z uprawnieniami toomanage i hello **ServiceBusContract** klasy jest jedynym punktem hello komunikacji przy użyciu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="eb1ed-129">Witaj **ServiceBusService** klasa dostarcza metody toocreate, wyliczania i usuwania tematów.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="eb1ed-130">powitania po przykładzie pokazano, jak **ServiceBusService** obiekt może być używane toocreate temat o nazwie `TestTopic`, przestrzeń nazw o nazwie `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="eb1ed-131">Istnieją metody na **TopicInfo** umożliwiających hello tematu, należy ustawić wartość właściwości (na przykład: tooset hello domyślny czas wygaśnięcia (TTL) wartość toobe stosowane toomessages wysyłane toohello tematu).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="eb1ed-132">Witaj poniższy przykład przedstawia sposób toocreate temat o nazwie `TestTopic` o maksymalnym rozmiarze 5 GB:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="eb1ed-133">Należy pamiętać, których można używać hello **listTopics** metoda **ServiceBusContract** obiekty toocheck, jeśli temat o określonej nazwie już istnieje w przestrzeni nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="eb1ed-134">Tworzenie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eb1ed-134">Create subscriptions</span></span>
<span data-ttu-id="eb1ed-135">Subskrypcje tootopics również są tworzone za pomocą hello **ServiceBusService** klasy.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="eb1ed-136">Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji toohello hello.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="eb1ed-137">Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello</span><span class="sxs-lookup"><span data-stu-id="eb1ed-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="eb1ed-138">Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="eb1ed-139">Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="eb1ed-140">Witaj poniższy przykład tworzy subskrypcję o nazwie "AllMessages" i używa hello domyślne **MatchAll** filtru.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="eb1ed-141">Tworzenie subskrypcji z filtrami</span><span class="sxs-lookup"><span data-stu-id="eb1ed-141">Create subscriptions with filters</span></span>
<span data-ttu-id="eb1ed-142">Można również utworzyć filtry, które pozwalają tooscope wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="eb1ed-143">Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest [SqlFilter][SqlFilter], która implementuje podzbiór standardu SQL92.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="eb1ed-144">Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="eb1ed-145">Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="eb1ed-146">Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają niestandardowy **MessageNumber** Właściwość jest większy niż 3:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="eb1ed-147">Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają **MessageNumber** Właściwość mniejszą lub równą too3:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="eb1ed-148">Kiedy wiadomość jest teraz wysyłane za`TestTopic`, będzie można zawsze dostarczyć toohello tooreceivers subskrybowane `AllMessages` subskrypcji i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` (subskrypcji w zależności od zawartości komunikatu).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="eb1ed-149">Wysyłanie wiadomości tooa tematu</span><span class="sxs-lookup"><span data-stu-id="eb1ed-149">Send messages tooa topic</span></span>
<span data-ttu-id="eb1ed-150">uzyskuje aplikacji toosend tematu komunikatów usługi Service Bus tooa **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="eb1ed-151">Witaj poniższy kod przedstawia sposób toosend wiadomość hello `TestTopic` temat wcześniej utworzone w ramach hello `HowToSample` przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="eb1ed-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="eb1ed-152">Komunikaty wysyłane tematy magistrali tooService są wystąpieniami klasy [BrokeredMessage] [ BrokeredMessage] klasy.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="eb1ed-153">[BrokeredMessage][BrokeredMessage]* obiekty mają zestaw metod standardowych (takich jak **setLabel** i **TimeToLive**), słownik, który jest używany toohold niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="eb1ed-154">Aplikacja może ustawić hello treść komunikatu przez przekazanie dowolnego obiektu podlegającego serializacji do konstruktora hello [BrokeredMessage][BrokeredMessage]i odpowiednie hello **DataContractSerializer**  będzie używana tooserialize hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="eb1ed-155">Alternatywnie **java.io.InputStream** można podać.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="eb1ed-156">Witaj poniższym przykładzie pokazano, jak testu toosend pięciu komunikatów toothe `TestTopic` **MessageSender** możemy uzyskać we fragmencie kodu hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="eb1ed-157">Uwaga jak hello **MessageNumber** wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (umożliwi to określenie subskrypcje, które go otrzymają):</span><span class="sxs-lookup"><span data-stu-id="eb1ed-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="eb1ed-158">Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="eb1ed-159">Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="eb1ed-160">Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="eb1ed-161">Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="eb1ed-162">Jak tooreceive komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eb1ed-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="eb1ed-163">tooreceive komunikatów z subskrypcji, użyj **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="eb1ed-164">Odebrane komunikaty mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="eb1ed-165">Korzystając z hello **ReceiveAndDelete** trybie odbieranie jest operacją pojedynczego zrzutu - oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu, oznacza hello komunikat jako wykorzystany i zwraca go toothe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="eb1ed-166">**ReceiveAndDelete** tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="eb1ed-167">toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="eb1ed-168">Ponieważ usługi Service Bus będzie zostały oznaczone komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="eb1ed-169">W **PeekLock** trybie odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="eb1ed-170">Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="eb1ed-171">Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu **usunąć** na wiadomość powitania odebrane.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="eb1ed-172">Kiedy Usługa Service Bus widzi hello **usunąć** wywołanie, go oznaczyć hello komunikat jako wykorzystany i usunąć go z tematu hello.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="eb1ed-173">Witaj na poniższym przykładzie przedstawiono sposób mogą być odbierane wiadomości i przetworzone przy użyciu **PeekLock** trybu (nie hello tryb domyślny).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="eb1ed-174">Witaj w poniższym przykładzie wykonuje pętlę i przetwarza wiadomości w subskrypcji "HighMessages" hello i kończy pracę, gdy nie ma żadnych więcej komunikatów (możesz też go mógł zostać ustawiony toowait nowe wiadomości).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

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
            // Display hello topic message.
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
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="eb1ed-175">Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości</span><span class="sxs-lookup"><span data-stu-id="eb1ed-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="eb1ed-176">Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="eb1ed-177">Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **unlockMessage** metody na wiadomość powitania odebranych (zamiast hello **deleteMessage** metody).</span><span class="sxs-lookup"><span data-stu-id="eb1ed-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="eb1ed-178">Spowoduje to, że wiadomość hello toounlock usługi Service Bus w temacie hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="eb1ed-179">Istnieje również limit czasu skojarzony z komunikatem zablokowanym w temacie, a jeśli awarii aplikacji hello wiadomość hello tooprocess przed przekroczenie limitu czasu blokady upływem (na przykład jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="eb1ed-180">W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **deleteMessage** żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="eb1ed-181">Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="eb1ed-182">Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="eb1ed-183">Jest to często osiągane przy użyciu hello **getMessageId** metody wiadomość hello, która pozostaje niezmienna między kolejnymi próbami dostarczenia.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="eb1ed-184">Usuwanie tematów i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eb1ed-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="eb1ed-185">Witaj podstawowy sposób toodelete tematy i subskrypcje jest toouse **ServiceBusContract** obiektu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="eb1ed-186">Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="eb1ed-187">Subskrypcje mogą być również usuwane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="eb1ed-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb1ed-188">Next Steps</span></span>
<span data-ttu-id="eb1ed-189">Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejek usługi Service Bus, tematy i subskrypcje] [ Service Bus queues, topics, and subscriptions] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="eb1ed-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
