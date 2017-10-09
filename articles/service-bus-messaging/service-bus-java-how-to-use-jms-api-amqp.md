---
title: "aaaHow toouse protokołu AMQP 1.0 z hello interfejsu API języka Java Service Bus | Dokumentacja firmy Microsoft"
description: "Jak toouse hello Java wiadomości usługi (JMS) z usługi Azure Service Bus i zaawansowane komunikatów usługi kolejkowania wiadomości Protodol (AMQP) 1.0."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="02192-103">Jak toouse hello Java wiadomości usługi (JMS) interfejsu API z usługi Service Bus i protokołu AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="02192-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="02192-104">Hello zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) 1.0 jest wydajne, niezawodne i poziom przesyłania komunikatów protokołu służy toobuild niezawodne, i platform aplikacji do obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="02192-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="02192-105">Obsługa protokołu AMQP 1.0 w usłudze Service Bus oznacza, że można użyć hello usługi kolejkowania wiadomości i publikowania/subskrypcji obsługiwanych przez brokera obsługi komunikatów funkcje z zakresu od platformy przy użyciu protokołu binarnego wydajne.</span><span class="sxs-lookup"><span data-stu-id="02192-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="02192-106">Ponadto można tworzyć aplikacje obejmuje składniki utworzony przy użyciu różnych języków, struktur i systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="02192-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="02192-107">W tym artykule opisano, jak toouse funkcji usługi Service Bus obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) z aplikacji języka Java przy użyciu hello protokół popularnych Java wiadomości usługi (JMS) w standardowe interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="02192-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="02192-108">Brak [artykułu Pomocnika](service-bus-amqp-dotnet.md) objaśniający sposób toodo hello tego samego, przy użyciu interfejsu API usługi Service Bus .NET hello.</span><span class="sxs-lookup"><span data-stu-id="02192-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="02192-109">Możesz użyć tych toolearn razem dwa przewodniki dotyczące obsługi wielu platform wiadomości przy użyciu protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="02192-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="02192-110">Rozpoczynanie pracy z usługą Service Bus</span><span class="sxs-lookup"><span data-stu-id="02192-110">Get started with Service Bus</span></span>
<span data-ttu-id="02192-111">W tym przewodniku założono, że już przestrzeń nazw magistrali usług zawierający kolejki o nazwie **kolejki Kolejka1**.</span><span class="sxs-lookup"><span data-stu-id="02192-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="02192-112">Jeśli nie chcesz, możesz [tworzenie przestrzeni nazw hello i kolejki](service-bus-create-namespace-portal.md) przy użyciu hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02192-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="02192-113">Aby uzyskać więcej informacji na temat sposobu przestrzeni nazw usługi Service Bus toocreate i kolejek, zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="02192-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="02192-114">Partycjonowane kolejki i tematy obsługują także protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="02192-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="02192-115">Aby uzyskać więcej informacji, zobacz [partycjonowane jednostki do obsługi komunikatów](service-bus-partitioning.md) i [obsługi protokołu AMQP 1.0 dla usługi Service Bus podzielona na partycje, kolejek i tematów](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02192-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="02192-116">Biblioteka klienta protokołu AMQP 1.0 JMS hello pobierania</span><span class="sxs-lookup"><span data-stu-id="02192-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="02192-117">Informacje o którym toodownload hello najnowszej wersji biblioteki klienta hello Apache Qpid JMS protokołu AMQP 1.0, można znaleźć [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="02192-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="02192-118">Należy dodać następujące cztery pliki JAR z hello Apache Qpid JMS protokołu AMQP 1.0 dystrybucji archiwum toohello klasy Java, podczas tworzenia i uruchamiania aplikacji JMS za pomocą usługi Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="02192-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="02192-119">geronimo jms\_1.1\_1.0.jar specyfikacji</span><span class="sxs-lookup"><span data-stu-id="02192-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="02192-120">qpid-amqp-1-0-Client-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="02192-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="02192-121">qpid-amqp-1-0-Client-jms-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="02192-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="02192-122">qpid-amqp-1-0-Common-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="02192-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="02192-123">Kodowanie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="02192-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="02192-124">Nazewnictwo Java i katalog interfejsu (JNDI)</span><span class="sxs-lookup"><span data-stu-id="02192-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="02192-125">JMS używa hello nazywania Java i katalog interfejsu (JNDI) toocreate rozdzielenie nazwy logicznej i fizycznej.</span><span class="sxs-lookup"><span data-stu-id="02192-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="02192-126">Dwa typy obiektów JMS są rozpoznawane przy użyciu JNDI: ConnectionFactory i docelowego.</span><span class="sxs-lookup"><span data-stu-id="02192-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="02192-127">JNDI korzysta z modelu dostawcy, w którym można podłączyć innego katalogu usługi toohandle Nazwa rozwiązania obowiązków.</span><span class="sxs-lookup"><span data-stu-id="02192-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="02192-128">Witaj Apache Qpid JMS protokołu AMQP 1.0 biblioteka zawiera proste właściwości opartych na plikach JNDI dostawcy, który jest skonfigurowany przy użyciu pliku właściwości hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="02192-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="02192-129">Skonfiguruj hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="02192-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="02192-130">Witaj toodefine wpis **ConnectionFactory** w hello Qpid właściwości pliku JNDI dostawcy jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="02192-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="02192-131">Gdzie **[jndi_name]** i **[ConnectionURL]** mają następujące znaczenie hello:</span><span class="sxs-lookup"><span data-stu-id="02192-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="02192-132">**[jndi_name]** : hello nazwę logiczną hello ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="02192-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="02192-133">To jest nazwa hello zostaną rozwiązane w aplikacji Java hello przy użyciu metody JNDI IntialContext.lookup() hello.</span><span class="sxs-lookup"><span data-stu-id="02192-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="02192-134">**[ConnectionURL]** : Adres URL, który dostarcza informacji hello hello JMS biblioteki wymagane toohello AMQP brokera.</span><span class="sxs-lookup"><span data-stu-id="02192-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="02192-135">Hello format hello **ConnectionURL** wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="02192-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="02192-136">Gdzie **[przestrzeń nazw]**, **[SASPolicyName]** i **[SASPolicyKey]** mają następujące znaczenie hello:</span><span class="sxs-lookup"><span data-stu-id="02192-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="02192-137">**[przestrzeń nazw]** : hello przestrzeń nazw magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="02192-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="02192-138">**[SASPolicyName]** : Nazwa zasady hello sygnatura dostępu współdzielonego dla kolejki.</span><span class="sxs-lookup"><span data-stu-id="02192-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="02192-139">**[SASPolicyKey]** : klucz zasad hello sygnatura dostępu współdzielonego dla kolejki.</span><span class="sxs-lookup"><span data-stu-id="02192-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="02192-140">Należy ręcznie hasła hello kodowania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="02192-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="02192-141">Przydatne narzędzie kodowania adresu URL jest dostępna na [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="02192-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="02192-142">Konfigurowanie miejsc docelowych</span><span class="sxs-lookup"><span data-stu-id="02192-142">Configure destinations</span></span>
<span data-ttu-id="02192-143">wpis Hello używany toodefine jest obiektem docelowym jest hello Qpid właściwości pliku JNDI dostawcy hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="02192-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="02192-144">lub</span><span class="sxs-lookup"><span data-stu-id="02192-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="02192-145">Gdzie **[jndi\_nazwę]** i **[fizycznych\_name]** mają następujące znaczenie hello:</span><span class="sxs-lookup"><span data-stu-id="02192-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="02192-146">**[jndi_name]** : hello nazwy logicznej hello przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="02192-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="02192-147">To jest nazwa hello zostaną rozwiązane w aplikacji Java hello przy użyciu metody JNDI IntialContext.lookup() hello.</span><span class="sxs-lookup"><span data-stu-id="02192-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="02192-148">**[physical_name]** : Nazwa hello hello aplikacji hello toowhich jednostek usługi Service Bus wysłania lub odebrania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="02192-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="02192-149">Podczas odbierania z subskrypcję tematu usługi Service Bus, hello nazwa fizycznego określony w JNDI powinna być nazwą hello hello tematu.</span><span class="sxs-lookup"><span data-stu-id="02192-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="02192-150">Nazwa subskrypcji Hello podano po utworzeniu subskrypcji trwałe hello hello JMS kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02192-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="02192-151">Witaj [Service Bus protokołu AMQP 1.0 przewodnik dewelopera](service-bus-amqp-dotnet.md) zawiera więcej szczegółowych informacji dotyczących pracy z tematów usługi Service Bus z JMS.</span><span class="sxs-lookup"><span data-stu-id="02192-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="02192-152">Pisanie aplikacji JMS hello</span><span class="sxs-lookup"><span data-stu-id="02192-152">Write hello JMS application</span></span>
<span data-ttu-id="02192-153">Nie ma żadnych specjalnych interfejsów API lub opcje potrzebne podczas korzystania z usługi Service Bus JMS.</span><span class="sxs-lookup"><span data-stu-id="02192-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="02192-154">Istnieje jednak kilka ograniczeń, które zostały omówione później.</span><span class="sxs-lookup"><span data-stu-id="02192-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="02192-155">Podobnie jak w dowolnej aplikacji JMS powitania po pierwsze wymagane jest konfiguracji środowiska JNDI hello, w stanie tooresolve toobe **ConnectionFactory** i miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="02192-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="02192-156">Skonfiguruj hello JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="02192-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="02192-157">Witaj JNDI środowisko jest skonfigurowane przez przekazanie do hello Konstruktor klasy javax.naming.InitialContext hello hashtable informacji o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="02192-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="02192-158">Witaj dwóch wymaganych elementów w obiekcie hashtable hello są nazwa klasy hello hello początkowej fabryki kontekstu i hello adres URL dostawcy.</span><span class="sxs-lookup"><span data-stu-id="02192-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="02192-159">Witaj poniższy kod pokazuje, jak tooconfigure hello JNDI środowiska toouse hello Qpid właściwości pliku JNDI dostawcy z plikiem właściwości o nazwie **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="02192-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="02192-160">Prostą aplikację JMS przy użyciu kolejki usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="02192-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="02192-161">Witaj następujący przykład program wysyła kolejki usługi Service Bus tooa JMS TextMessages z nazwy logicznej JNDI hello kolejki i odbiera wiadomości powitania ponownie.</span><span class="sxs-lookup"><span data-stu-id="02192-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a><span data-ttu-id="02192-162">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="02192-162">Run hello application</span></span>
<span data-ttu-id="02192-163">Uruchomienie aplikacji hello generuje dane wyjściowe w formie hello:</span><span class="sxs-lookup"><span data-stu-id="02192-163">Running hello application produces output of hello form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="02192-164">Wysyłanie komunikatów między JMS i .NET wielu platform</span><span class="sxs-lookup"><span data-stu-id="02192-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="02192-165">W tym przewodniku pokazano, jak toosend i odbieranie wiadomości tooand z usługi Service Bus przy użyciu JMS.</span><span class="sxs-lookup"><span data-stu-id="02192-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="02192-166">Jedną z kluczowych zalet protokołu AMQP 1.0 hello jest jednak możliwość toobe aplikacje zbudowane na podstawie składników zapisany w różnych językach, za pomocą wiadomości wymieniane niezawodne i w pełnej rozdzielczości.</span><span class="sxs-lookup"><span data-stu-id="02192-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="02192-167">Przy użyciu aplikacji JMS przykładowej hello opisane powyżej i podobnych aplikacji .NET z artykułu pomocnika, [przy użyciu usługi Service Bus z .NET z protokołu AMQP 1.0](service-bus-amqp-dotnet.md), mogą wymieniać komunikaty między .NET i Java.</span><span class="sxs-lookup"><span data-stu-id="02192-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="02192-168">Przeczytaj ten artykuł, aby uzyskać więcej informacji o szczegóły hello wieloplatformowych wiadomości przy użyciu usługi Service Bus i protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="02192-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="02192-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="02192-169">JMS too.NET</span></span>
<span data-ttu-id="02192-170">toodemonstrate JMS too.NET wiadomości:</span><span class="sxs-lookup"><span data-stu-id="02192-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="02192-171">Uruchom hello .NET przykładowej aplikacji bez żadnych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="02192-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="02192-172">Z argumentem wiersza polecenia "sendonly" hello, należy uruchomić hello Java przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02192-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="02192-173">W tym trybie hello aplikacji nie będą otrzymywać wiadomości z kolejki hello tylko wysyła.</span><span class="sxs-lookup"><span data-stu-id="02192-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="02192-174">Naciśnij klawisz **Enter** kilka razy w konsoli aplikacji Java hello, który spowoduje, że toobe wiadomości wysyłane.</span><span class="sxs-lookup"><span data-stu-id="02192-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="02192-175">Te komunikaty są odbierane przez hello aplikacji .NET.</span><span class="sxs-lookup"><span data-stu-id="02192-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="02192-176">Dane wyjściowe aplikacji JMS</span><span class="sxs-lookup"><span data-stu-id="02192-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="02192-177">Dane wyjściowe aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="02192-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="02192-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="02192-178">.NET tooJMS</span></span>
<span data-ttu-id="02192-179">tooJMS .NET toodemonstrate wiadomości:</span><span class="sxs-lookup"><span data-stu-id="02192-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="02192-180">Z argumentem wiersza polecenia "sendonly" hello, należy uruchomić hello .NET przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02192-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="02192-181">W tym trybie hello aplikacji nie będą otrzymywać wiadomości z kolejki hello tylko wysyła.</span><span class="sxs-lookup"><span data-stu-id="02192-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="02192-182">Uruchom hello Java przykładowej aplikacji bez żadnych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="02192-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="02192-183">Naciśnij klawisz **Enter** kilka razy w hello konsoli aplikacji .NET, który spowoduje, że toobe wiadomości wysyłane.</span><span class="sxs-lookup"><span data-stu-id="02192-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="02192-184">Te komunikaty są odbierane przez hello aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="02192-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="02192-185">Dane wyjściowe aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="02192-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="02192-186">Dane wyjściowe aplikacji JMS</span><span class="sxs-lookup"><span data-stu-id="02192-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="02192-187">Nieobsługiwane funkcje i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="02192-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="02192-188">Podczas przy użyciu JMS za pośrednictwem protokołu AMQP 1.0 z usługą Service Bus, a mianowicie istnieją Hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="02192-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="02192-189">Tylko jeden **MessageProducer** lub **MessageConsumer** dozwolone jest używanie **sesji**.</span><span class="sxs-lookup"><span data-stu-id="02192-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="02192-190">Jeśli potrzebujesz toocreate wiele **MessageProducers** lub **MessageConsumers** w aplikacji, Utwórz dedykowana **sesji** dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="02192-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="02192-191">Subskrypcje tematu nietrwałe nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="02192-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="02192-192">**MessageSelectors** nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="02192-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="02192-193">Tymczasowe miejsc docelowych; na przykład **TemporaryQueue**, **TemporaryTopic** nie są obecnie obsługiwane, wraz z hello **QueueRequestor** i **TopicRequestor**Interfejsów API, które z nich korzystają.</span><span class="sxs-lookup"><span data-stu-id="02192-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="02192-194">Transakcyjne sesji i transakcje rozproszone nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="02192-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="02192-195">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="02192-195">Summary</span></span>
<span data-ttu-id="02192-196">Ten temat tooguide pokazano, jak toouse funkcji usługi Service Bus obsługiwanych przez brokera obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) z języka Java przy użyciu hello popularnych JMS interfejsu API i protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="02192-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="02192-197">Umożliwia także Service Bus protokołu AMQP 1.0 z innych języków, w tym .NET, C, Python i PHP.</span><span class="sxs-lookup"><span data-stu-id="02192-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="02192-198">Składniki utworzone przy użyciu tych języków mogą wymieniać komunikaty, niezawodne i w pełnej rozdzielczości, przy użyciu obsługi hello protokołu AMQP 1.0 w usłudze Service Bus.</span><span class="sxs-lookup"><span data-stu-id="02192-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02192-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02192-199">Next steps</span></span>
* [<span data-ttu-id="02192-200">Obsługa protokołu AMQP 1.0 w Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="02192-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="02192-201">Jak toouse protokołu AMQP 1.0 z hello interfejsu API usługi Service Bus .NET</span><span class="sxs-lookup"><span data-stu-id="02192-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="02192-202">Service Bus protokołu AMQP 1.0 przewodnik dewelopera</span><span class="sxs-lookup"><span data-stu-id="02192-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="02192-203">Wprowadzenie do kolejek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="02192-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="02192-204">Centrum deweloperów języka Java</span><span class="sxs-lookup"><span data-stu-id="02192-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

