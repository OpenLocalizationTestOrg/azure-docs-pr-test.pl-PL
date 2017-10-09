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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Jak toouse usługi Service Bus tematów i subskrypcji z językiem Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

W tym przewodniku opisano sposób toouse usługi Service Bus tematów i subskrypcji. Hello przykłady są napisane w języku Java i używają hello [zestawu Azure SDK dla języka Java][Azure SDK for Java]. Witaj omówione scenariusze obejmują **tworzenie tematów i subskrypcji**, **tworzenie filtrów subskrypcji**, **wysyłania wiadomości tooa tematu**, **odbieranie komunikaty z subskrypcji**, i **usuwanie tematów i subskrypcji**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Co to są tematy i subskrypcje usługi Service Bus?
Tematy i subskrypcje usługi Service Bus obsługują model komunikacji z użyciem *publikowania/subskrypcji* komunikatów. Podczas korzystania z tematów i subskrypcji składniki aplikacji rozproszonej nie komunikują się bezpośrednio ze sobą, lecz wymieniają komunikaty za pośrednictwem tematu, która działa jako pośrednik.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

W przeciwieństwie do kolejek usługi Service Bus, w których każdy komunikat jest przetwarzany przez jednego konsumenta, tematy i subskrypcje zapewniają formę komunikacji „jeden do wielu” z użyciem wzorca publikowania/subskrypcji. Istnieje możliwość zarejestrowania wielu subskrypcji tooa tematu. Jeżeli tooa tematu jest wysyłany komunikat, jest następnie on proces toohandle subskrypcji tooeach dostępne niezależnie.

Temat tooa subskrypcji przypomina wirtualną kolejkę, która odbiera kopie wiadomości powitania, które zostały wysłane toohello tematu. Opcjonalnie można zarejestrować reguły filtrów dla tematu oparte na subskrypcji, dzięki czemu można toofilter/ograniczyć które tematu tooa komunikaty są odbierane przez poszczególne subskrypcje.

Tematy usługi Service Bus i subskrypcje pozwalają tooprocess tooscale bardzo dużej liczby komunikatów w bardzo dużej liczby użytkowników i aplikacji.

## <a name="create-a-service-namespace"></a>Tworzenie przestrzeni nazw usługi
toobegin przy użyciu usługi Service Bus tematów i subskrypcji platformy Azure, musisz najpierw utworzyć przestrzeń nazw zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.

toocreate przestrzeni nazw:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci toouse aplikacji usługi Service Bus
Upewnij się, że zainstalowano hello [zestawu Azure SDK dla języka Java] [ Azure SDK for Java] przed zbudowaniem tego przykładu. Jeśli używasz programu Eclipse, można zainstalować hello [zestawu narzędzi platformy Azure dla programu Eclipse] [ Azure Toolkit for Eclipse] zawierającą hello Azure SDK dla języka Java. Następnie można dodać hello **bibliotek usługi Microsoft Azure dla języka Java** tooyour projektu:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Dodaj następujące hello `import` toohello instrukcje na początku pliku Java hello:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Dodaj hello biblioteki Azure dla języka Java tooyour zbudować ścieżki i uwzględnić go w tym zestawem wdrażania projektu.

## <a name="create-a-topic"></a>Tworzenie tematu
Operacje zarządzania dla tematów usługi Service Bus można wykonywać za pomocą **ServiceBusContract** klasy. A **ServiceBusContract** obiekt jest tworzony z odpowiednią konfiguracją, która hermetyzuje tokenu sygnatury dostępu Współdzielonego z uprawnieniami toomanage i hello **ServiceBusContract** klasy jest jedynym punktem hello komunikacji przy użyciu platformy Azure.

Witaj **ServiceBusService** klasa dostarcza metody toocreate, wyliczania i usuwania tematów. powitania po przykładzie pokazano, jak **ServiceBusService** obiekt może być używane toocreate temat o nazwie `TestTopic`, przestrzeń nazw o nazwie `HowToSample`:

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

Istnieją metody na **TopicInfo** umożliwiających hello tematu, należy ustawić wartość właściwości (na przykład: tooset hello domyślny czas wygaśnięcia (TTL) wartość toobe stosowane toomessages wysyłane toohello tematu). Witaj poniższy przykład przedstawia sposób toocreate temat o nazwie `TestTopic` o maksymalnym rozmiarze 5 GB:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Należy pamiętać, których można używać hello **listTopics** metoda **ServiceBusContract** obiekty toocheck, jeśli temat o określonej nazwie już istnieje w przestrzeni nazw usługi.

## <a name="create-subscriptions"></a>Tworzenie subskrypcji
Subskrypcje tootopics również są tworzone za pomocą hello **ServiceBusService** klasy. Subskrypcje są nazywane i mogą zawierać opcjonalny filtr, który ogranicza zestaw komunikatów przesyłany do wirtualnej kolejki subskrypcji toohello hello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Tworzenie subskrypcji z filtrem domyślnym (MatchAll) hello
Witaj **MatchAll** filtr jest filtrem domyślnym hello, który zostanie użyty, jeśli został określony żaden filtr, podczas tworzenia nowej subskrypcji. Gdy hello **MatchAll** filtr jest używany, wszystkie komunikaty opublikowane toohello tematu są umieszczane w wirtualnej kolejce subskrypcji. Witaj poniższy przykład tworzy subskrypcję o nazwie "AllMessages" i używa hello domyślne **MatchAll** filtru.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Tworzenie subskrypcji z filtrami
Można również utworzyć filtry, które pozwalają tooscope wysłane wiadomości, które powinny być widoczne tooa tematu w subskrypcji określonego tematu.

Witaj najbardziej elastycznym typem filtru obsługiwanym przez subskrypcje jest [SqlFilter][SqlFilter], która implementuje podzbiór standardu SQL92. Filtry SQL działają na powitania właściwości wiadomości powitania, które są opublikowane toohello tematu. Aby uzyskać więcej informacji na temat hello wyrażeń, które mogą być używane z filtrem SQL, przejrzyj hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] składni.

Witaj poniższy przykład tworzy subskrypcję o nazwie `HighMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają niestandardowy **MessageNumber** Właściwość jest większy niż 3:

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

Podobnie, hello poniższy przykład tworzy subskrypcję o nazwie `LowMessages` z [SqlFilter] [ SqlFilter] obiekt, który wybiera tylko komunikaty, które mają **MessageNumber** Właściwość mniejszą lub równą too3:

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

Kiedy wiadomość jest teraz wysyłane za`TestTopic`, będzie można zawsze dostarczyć toohello tooreceivers subskrybowane `AllMessages` subskrypcji i selektywnie dostarczany tooreceivers subskrybowane toohello `HighMessages` i `LowMessages` (subskrypcji w zależności od zawartości komunikatu).

## <a name="send-messages-tooa-topic"></a>Wysyłanie wiadomości tooa tematu
uzyskuje aplikacji toosend tematu komunikatów usługi Service Bus tooa **ServiceBusContract** obiektu. Witaj poniższy kod przedstawia sposób toosend wiadomość hello `TestTopic` temat wcześniej utworzone w ramach hello `HowToSample` przestrzeni nazw:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

Komunikaty wysyłane tematy magistrali tooService są wystąpieniami klasy [BrokeredMessage] [ BrokeredMessage] klasy. [BrokeredMessage][BrokeredMessage]* obiekty mają zestaw metod standardowych (takich jak **setLabel** i **TimeToLive**), słownik, który jest używany toohold niestandardowych właściwości specyficzne dla aplikacji oraz treść dowolnych danych aplikacji. Aplikacja może ustawić hello treść komunikatu przez przekazanie dowolnego obiektu podlegającego serializacji do konstruktora hello [BrokeredMessage][BrokeredMessage]i odpowiednie hello **DataContractSerializer**  będzie używana tooserialize hello obiektu. Alternatywnie **java.io.InputStream** można podać.

Witaj poniższym przykładzie pokazano, jak testu toosend pięciu komunikatów toothe `TestTopic` **MessageSender** możemy uzyskać we fragmencie kodu hello powyżej.
Uwaga jak hello **MessageNumber** wartość właściwości każdego komunikatu różni się na powitania iteracji pętli hello (umożliwi to określenie subskrypcje, które go otrzymają):

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

Tematy usługi Service Bus obsługują maksymalny rozmiar komunikatu 256 KB w hello [warstwy standardowa](service-bus-premium-messaging.md) i 1 MB w hello [warstwy Premium](service-bus-premium-messaging.md). Nagłówek Hello, który zawiera standardowy hello i właściwości niestandardowych aplikacji, może mieć maksymalny rozmiar 64 KB. Nie ma żadnego limitu na powitania liczby komunikatów w temacie, ale jest ograniczenie całkowitego rozmiaru przechowywanych przez temat wiadomości powitania hello. Rozmiar tematu jest definiowany w czasie tworzenia, z górnym limitem 5 GB.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Jak tooreceive komunikatów z subskrypcji
tooreceive komunikatów z subskrypcji, użyj **ServiceBusContract** obiektu. Odebrane komunikaty mogą pracować w dwóch różnych trybach: **ReceiveAndDelete** i **PeekLock**.

Korzystając z hello **ReceiveAndDelete** trybie odbieranie jest operacją pojedynczego zrzutu - oznacza to, kiedy usługa Service Bus odbiera żądanie odczytu komunikatu, oznacza hello komunikat jako wykorzystany i zwraca go toothe aplikacji. **ReceiveAndDelete** tryb hello najprostszym modelem i działa najlepiej w scenariuszach, w których aplikacja może tolerować nieprzetworzenie komunikatu w razie awarii hello. toounderstand, Rozważmy scenariusz w problemy, które konsumenta hello hello mógł odebrać żądanie, a następnie ulega awarii przed jego przetworzeniem. Ponieważ usługi Service Bus będzie zostały oznaczone komunikat jako wykorzystany, następnie podczas aplikacji hello uruchamia ponownie i rozpoczyna się ponownie korzystanie z komunikatów, pominie utracony wiadomości powitania, który został wykorzystany przed toohello awarii.

W **PeekLock** trybie odbieranie staje się operacją dwuetapowy, dzięki czemu możliwe toosupport aplikacji, które nie tolerują brakujących komunikatów. Usługa Service Bus odbiera żądanie, znajduje się dalej toobe wiadomość hello używane, blokuje go tooprevent innym klientom odebrania go i zwraca go po toohello aplikacji. Kiedy aplikacja hello zakończy przetwarzanie wiadomości powitania (lub niezawodnie zapisze go w celu przyszłego przetwarzania), wykonuje drugi etap hello hello odbierania przez wywołanie metody procesu **usunąć** na wiadomość powitania odebrane. Kiedy Usługa Service Bus widzi hello **usunąć** wywołanie, go oznaczyć hello komunikat jako wykorzystany i usunąć go z tematu hello.

Witaj na poniższym przykładzie przedstawiono sposób mogą być odbierane wiadomości i przetworzone przy użyciu **PeekLock** trybu (nie hello tryb domyślny). Witaj w poniższym przykładzie wykonuje pętlę i przetwarza wiadomości w subskrypcji "HighMessages" hello i kończy pracę, gdy nie ma żadnych więcej komunikatów (możesz też go mógł zostać ustawiony toowait nowe wiadomości).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Jak wystąpiła awaria aplikacji toohandle i nie można go odczytać wiadomości
Usługa Service Bus udostępnia toohelp funkcji, które bezpieczne odzyskiwanie w razie błędów w aplikacji lub trudności z przetwarzaniem komunikatu. Jeśli aplikacja odbiorcy nie tooprocess hello komunikat dla jakiegoś powodu, wówczas może wywołać hello **unlockMessage** metody na wiadomość powitania odebranych (zamiast hello **deleteMessage** metody). Spowoduje to, że wiadomość hello toounlock usługi Service Bus w temacie hello i stał się dostępny toobe odbioru, albo hello przez sam korzystanie z aplikacji lub inną odbierającą aplikację.

Istnieje również limit czasu skojarzony z komunikatem zablokowanym w temacie, a jeśli awarii aplikacji hello wiadomość hello tooprocess przed przekroczenie limitu czasu blokady upływem (na przykład jeśli wystąpiła awaria aplikacji hello), Usługa Service Bus spowoduje automatyczne odblokowywanie wiadomość hello i stał się dostępny toobe odbioru.

W hello zdarzenie, które aplikacji hello ulegnie awarii po przetworzeniu wiadomość hello, ale przed hello **deleteMessage** żądania, a następnie wiadomość hello jest przed przeniesieniem toohello aplikacji po jej ponownym uruchomieniu. Jest to często nazywane **przetwarzaniem co najmniej raz**, oznacza to, że każdy komunikat będzie przetwarzany co najmniej raz, ale w niektórych sytuacjach hello sam komunikat może być dostarczony ponownie. Jeśli hello scenariusz nie Toleruje dwukrotnego przetwarzania, deweloperzy aplikacji powinni dodać dodatkową logikę tootheir aplikacji toohandle dwukrotnego dostarczania komunikatów. Jest to często osiągane przy użyciu hello **getMessageId** metody wiadomość hello, która pozostaje niezmienna między kolejnymi próbami dostarczenia.

## <a name="delete-topics-and-subscriptions"></a>Usuwanie tematów i subskrypcji
Witaj podstawowy sposób toodelete tematy i subskrypcje jest toouse **ServiceBusContract** obiektu. Usunięcie tematu spowoduje również usunięcie subskrypcji, które są zarejestrowane w usłudze hello tematu. Subskrypcje mogą być również usuwane niezależnie.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello kolejek usługi Service Bus, zobacz [kolejek usługi Service Bus, tematy i subskrypcje] [ Service Bus queues, topics, and subscriptions] Aby uzyskać więcej informacji.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
