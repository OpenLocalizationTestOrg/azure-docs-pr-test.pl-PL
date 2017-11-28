---
title: "Jak używać protokołu AMQP 1.0 przy użyciu interfejsu API języka Java Service Bus | Dokumentacja firmy Microsoft"
description: "Jak używać usługi komunikat Java (JMS) z usługi Azure Service Bus i zaawansowane komunikatów usługi kolejkowania wiadomości Protodol (AMQP) 1.0."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="f7002-103">Jak używać języka Java wiadomości usługi (JMS) interfejsu API z usługi Service Bus i protokołu AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="f7002-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="f7002-104">Zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) 1.0 to wydajne, niezawodne i poziom przewodowy obsługi wiadomości protokół służy do tworzenia aplikacji wiadomości niezawodne, między platformami.</span><span class="sxs-lookup"><span data-stu-id="f7002-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="f7002-105">Obsługa dla protokołu AMQP 1.0 w usłudze Service Bus oznacza, że można użyć Kolejkowanie i publikowania/subskrypcji obsługiwanych przez brokera obsługi komunikatów funkcje z zakresu od platformy przy użyciu protokołu binarnego wydajne.</span><span class="sxs-lookup"><span data-stu-id="f7002-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="f7002-106">Ponadto można tworzyć aplikacje obejmuje składniki utworzony przy użyciu różnych języków, struktur i systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f7002-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="f7002-107">W tym artykule opisano sposób użycia funkcji (kolejki i tematy publikowania/subskrypcji) do obsługi komunikatów usługi Service Bus z aplikacji języka Java przy użyciu popularnych Java wiadomości usługi (JMS) interfejsu API standardowa.</span><span class="sxs-lookup"><span data-stu-id="f7002-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="f7002-108">Brak [artykułu Pomocnika](service-bus-amqp-dotnet.md) objaśniający sposób wykonaj te same przy użyciu interfejsu API usługi Service Bus .NET.</span><span class="sxs-lookup"><span data-stu-id="f7002-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="f7002-109">Umożliwia te dwa przewodniki razem więcej informacji na temat obsługi wiadomości między platformami przy użyciu protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="f7002-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="f7002-110">Rozpoczynanie pracy z usługą Service Bus</span><span class="sxs-lookup"><span data-stu-id="f7002-110">Get started with Service Bus</span></span>
<span data-ttu-id="f7002-111">W tym przewodniku założono, że już przestrzeń nazw magistrali usług zawierający kolejki o nazwie **kolejki Kolejka1**.</span><span class="sxs-lookup"><span data-stu-id="f7002-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="f7002-112">Jeśli nie chcesz, możesz [tworzenie przestrzeni nazw i kolejki](service-bus-create-namespace-portal.md) przy użyciu [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7002-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f7002-113">Aby uzyskać więcej informacji na temat tworzenia przestrzeni nazw usługi Service Bus i kolejek, zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="f7002-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f7002-114">Partycjonowane kolejki i tematy obsługują także protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="f7002-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="f7002-115">Aby uzyskać więcej informacji, zobacz [partycjonowane jednostki do obsługi komunikatów](service-bus-partitioning.md) i [obsługi protokołu AMQP 1.0 dla usługi Service Bus podzielona na partycje, kolejek i tematów](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f7002-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="f7002-116">Pobieranie biblioteki klienta protokołu AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="f7002-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="f7002-117">Aby dowiedzieć się, skąd pobrać najnowszej wersji biblioteki klienta Apache Qpid JMS protokołu AMQP 1.0, odwiedź stronę [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="f7002-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="f7002-118">Należy dodać następujące cztery pliki JAR z archiwum dystrybucji Apache Qpid JMS protokołu AMQP 1.0 do klasy Java podczas tworzenia i uruchamiania aplikacji JMS za pomocą usługi Service Bus:</span><span class="sxs-lookup"><span data-stu-id="f7002-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="f7002-119">geronimo jms\_1.1\_1.0.jar specyfikacji</span><span class="sxs-lookup"><span data-stu-id="f7002-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="f7002-120">qpid-amqp-1-0-Client-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="f7002-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="f7002-121">qpid-amqp-1-0-Client-jms-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="f7002-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="f7002-122">qpid-amqp-1-0-Common-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="f7002-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="f7002-123">Kodowanie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="f7002-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="f7002-124">Nazewnictwo Java i katalog interfejsu (JNDI)</span><span class="sxs-lookup"><span data-stu-id="f7002-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="f7002-125">JMS używa nazwy języka Java i katalog interfejsu (JNDI) do utworzenia rozdzielenie nazwy logicznej i fizycznej.</span><span class="sxs-lookup"><span data-stu-id="f7002-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="f7002-126">Dwa typy obiektów JMS są rozpoznawane przy użyciu JNDI: ConnectionFactory i docelowego.</span><span class="sxs-lookup"><span data-stu-id="f7002-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="f7002-127">JNDI korzysta z modelu dostawcy, w którym można podłączyć innego katalogu usługi do obsługi obowiązków rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="f7002-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="f7002-128">Format opartych na plikach JNDI dostawcy, który jest skonfigurowany przy użyciu pliku właściwości następujących Apache Qpid JMS protokołu AMQP 1.0 biblioteka zawiera proste właściwości:</span><span class="sxs-lookup"><span data-stu-id="f7002-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="f7002-129">Skonfiguruj ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="f7002-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="f7002-130">Używane do definiowania wpisu **ConnectionFactory** w pliku właściwości Qpid JNDI dostawcy jest następujący format:</span><span class="sxs-lookup"><span data-stu-id="f7002-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="f7002-131">Gdzie **[jndi_name]** i **[ConnectionURL]** mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="f7002-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="f7002-132">**[jndi_name]** : ConnectionFactory nazwę logiczną.</span><span class="sxs-lookup"><span data-stu-id="f7002-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="f7002-133">Jest to nazwa, która zostanie rozwiązany w aplikacji Java za pomocą metody JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="f7002-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="f7002-134">**[ConnectionURL]** : Adres URL, który zapewnia biblioteki JMS informacje wymagane do brokera protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="f7002-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="f7002-135">Format **ConnectionURL** wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="f7002-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="f7002-136">Gdzie **[przestrzeń nazw]**, **[SASPolicyName]** i **[SASPolicyKey]** mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="f7002-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="f7002-137">**[przestrzeń nazw]** : Przestrzeń nazw magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="f7002-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="f7002-138">**[SASPolicyName]** : Nazwa zasady sygnatura dostępu współdzielonego kolejki.</span><span class="sxs-lookup"><span data-stu-id="f7002-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="f7002-139">**[SASPolicyKey]** : Klucz zasad sygnatura dostępu współdzielonego kolejki.</span><span class="sxs-lookup"><span data-stu-id="f7002-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="f7002-140">Należy zakodować adres URL hasła ręcznie.</span><span class="sxs-lookup"><span data-stu-id="f7002-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="f7002-141">Przydatne narzędzie kodowania adresu URL jest dostępna na [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="f7002-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="f7002-142">Konfigurowanie miejsc docelowych</span><span class="sxs-lookup"><span data-stu-id="f7002-142">Configure destinations</span></span>
<span data-ttu-id="f7002-143">Wpis służy do definiowania miejsca docelowego w dostawcy JNDI Qpid właściwości plików ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="f7002-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="f7002-144">lub</span><span class="sxs-lookup"><span data-stu-id="f7002-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="f7002-145">Gdzie **[jndi\_name]** i **[fizycznych\_name]** mają następujące znaczenie:</span><span class="sxs-lookup"><span data-stu-id="f7002-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="f7002-146">**[jndi_name]** : Nazwy logicznej miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="f7002-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="f7002-147">Jest to nazwa, która zostanie rozwiązany w aplikacji Java za pomocą metody JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="f7002-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="f7002-148">**[physical_name]** : Nazwa jednostki magistrali usług, do którego wysyła lub odbiera komunikaty aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7002-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="f7002-149">Podczas odbierania z subskrypcję tematu usługi Service Bus, nazwa fizycznego określony w JNDI powinna być nazwę tematu.</span><span class="sxs-lookup"><span data-stu-id="f7002-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="f7002-150">Po utworzeniu subskrypcji trwałe w kodzie aplikacji JMS, jest podać nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f7002-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="f7002-151">[Service Bus protokołu AMQP 1.0 przewodnik dewelopera](service-bus-amqp-dotnet.md) zawiera więcej szczegółowych informacji dotyczących pracy z tematów usługi Service Bus z JMS.</span><span class="sxs-lookup"><span data-stu-id="f7002-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="f7002-152">Pisanie aplikacji JMS</span><span class="sxs-lookup"><span data-stu-id="f7002-152">Write the JMS application</span></span>
<span data-ttu-id="f7002-153">Nie ma żadnych specjalnych interfejsów API lub opcje potrzebne podczas korzystania z usługi Service Bus JMS.</span><span class="sxs-lookup"><span data-stu-id="f7002-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="f7002-154">Istnieje jednak kilka ograniczeń, które zostały omówione później.</span><span class="sxs-lookup"><span data-stu-id="f7002-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="f7002-155">Podobnie jak w dowolnej aplikacji JMS po pierwsze wymagana jest Konfiguracja środowiska JNDI, aby można było rozpoznać **ConnectionFactory** i miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="f7002-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="f7002-156">Skonfiguruj JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="f7002-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="f7002-157">Środowisko JNDI jest skonfigurowane przez przekazanie do konstruktora klasy javax.naming.InitialContext hashtable informacji o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f7002-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="f7002-158">Dwa wymaganych nazwę klasy początkowej fabryki kontekstu i adres URL dostawcy elementów w tablicy skrótów.</span><span class="sxs-lookup"><span data-stu-id="f7002-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="f7002-159">Poniższy kod przedstawia sposób konfigurowania środowiska JNDI do użycia Qpid dostawcy JNDI opartą na plikach właściwości z plikiem właściwości o nazwie **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="f7002-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="f7002-160">Prostą aplikację JMS przy użyciu kolejki usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="f7002-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="f7002-161">Następujący przykład program wysyła JMS TextMessages do kolejki usługi Service Bus z nazwy logicznej JNDI kolejki i odbiera komunikaty ponownie.</span><span class="sxs-lookup"><span data-stu-id="f7002-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="f7002-162">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7002-162">Run the application</span></span>
<span data-ttu-id="f7002-163">Uruchamianie aplikacji generuje dane wyjściowe w formie:</span><span class="sxs-lookup"><span data-stu-id="f7002-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="f7002-164">Wysyłanie komunikatów między JMS i .NET wielu platform</span><span class="sxs-lookup"><span data-stu-id="f7002-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="f7002-165">W tym przewodniku pokazano, jak wysyłać i odbierać komunikaty z magistrali usług przy użyciu JMS.</span><span class="sxs-lookup"><span data-stu-id="f7002-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="f7002-166">Jedną z kluczowych zalet protokołu AMQP 1.0 jest jednak umożliwia aplikacji ma zostać utworzony ze składników zapisany w różnych językach, za pomocą wiadomości wymieniane niezawodne i w pełnej rozdzielczości.</span><span class="sxs-lookup"><span data-stu-id="f7002-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="f7002-167">Za pomocą przykładowej aplikacji JMS opisane powyżej i podobnych aplikacji .NET z artykułu pomocnika, [przy użyciu usługi Service Bus z .NET z protokołu AMQP 1.0](service-bus-amqp-dotnet.md), mogą wymieniać komunikaty między .NET i Java.</span><span class="sxs-lookup"><span data-stu-id="f7002-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="f7002-168">Przeczytaj ten artykuł, aby uzyskać więcej informacji na temat szczegóły wieloplatformowych wiadomości przy użyciu usługi Service Bus i protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="f7002-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="f7002-169">JMS do .NET</span><span class="sxs-lookup"><span data-stu-id="f7002-169">JMS to .NET</span></span>
<span data-ttu-id="f7002-170">Aby zademonstrować JMS do obsługi komunikatów .NET:</span><span class="sxs-lookup"><span data-stu-id="f7002-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="f7002-171">Uruchom przykładową aplikację .NET bez żadnych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7002-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="f7002-172">Uruchom przykładową aplikację Java z argumentem wiersza polecenia "sendonly".</span><span class="sxs-lookup"><span data-stu-id="f7002-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="f7002-173">W tym trybie aplikacja nie będą otrzymywać wiadomości z kolejki, tylko wysyła.</span><span class="sxs-lookup"><span data-stu-id="f7002-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="f7002-174">Naciśnij klawisz **Enter** kilka razy w konsoli aplikacji Java, która spowoduje, że komunikatów do wysłania.</span><span class="sxs-lookup"><span data-stu-id="f7002-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="f7002-175">Te komunikaty są odbierane przez aplikację .NET.</span><span class="sxs-lookup"><span data-stu-id="f7002-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="f7002-176">Dane wyjściowe aplikacji JMS</span><span class="sxs-lookup"><span data-stu-id="f7002-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="f7002-177">Dane wyjściowe aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="f7002-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="f7002-178">.NET do JMS</span><span class="sxs-lookup"><span data-stu-id="f7002-178">.NET to JMS</span></span>
<span data-ttu-id="f7002-179">Aby zademonstrować .NET do obsługi komunikatów JMS:</span><span class="sxs-lookup"><span data-stu-id="f7002-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="f7002-180">Uruchom przykładową aplikację .NET z argumentem wiersza polecenia "sendonly".</span><span class="sxs-lookup"><span data-stu-id="f7002-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="f7002-181">W tym trybie aplikacja nie będą otrzymywać wiadomości z kolejki, tylko wysyła.</span><span class="sxs-lookup"><span data-stu-id="f7002-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="f7002-182">Uruchom przykładową aplikację Java bez żadnych argumentów wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7002-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="f7002-183">Naciśnij klawisz **Enter** kilka razy w aplikacji konsoli .NET, co spowoduje wyświetlanie komunikatów do wysłania.</span><span class="sxs-lookup"><span data-stu-id="f7002-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="f7002-184">Te komunikaty są odbierane przez aplikację Java.</span><span class="sxs-lookup"><span data-stu-id="f7002-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="f7002-185">Dane wyjściowe aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="f7002-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="f7002-186">Dane wyjściowe aplikacji JMS</span><span class="sxs-lookup"><span data-stu-id="f7002-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="f7002-187">Nieobsługiwane funkcje i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f7002-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="f7002-188">Korzystając z JMS za pośrednictwem protokołu AMQP 1.0 z usługą Service Bus, a mianowicie obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="f7002-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="f7002-189">Tylko jeden **MessageProducer** lub **MessageConsumer** dozwolone jest używanie **sesji**.</span><span class="sxs-lookup"><span data-stu-id="f7002-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="f7002-190">Jeśli trzeba utworzyć wiele **MessageProducers** lub **MessageConsumers** w aplikacji, Utwórz dedykowana **sesji** dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="f7002-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="f7002-191">Subskrypcje tematu nietrwałe nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f7002-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="f7002-192">**MessageSelectors** nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f7002-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="f7002-193">Tymczasowe miejsc docelowych; na przykład **TemporaryQueue**, **TemporaryTopic** nie są obecnie obsługiwane, wraz z **QueueRequestor** i **TopicRequestor**Interfejsów API, które z nich korzystają.</span><span class="sxs-lookup"><span data-stu-id="f7002-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="f7002-194">Transakcyjne sesji i transakcje rozproszone nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f7002-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="f7002-195">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f7002-195">Summary</span></span>
<span data-ttu-id="f7002-196">Ten przewodnik pokazano, jak używać funkcji usługi Service Bus obsługiwanych przez brokera obsługi komunikatów (kolejki i tematy publikowania/subskrypcji) za pomocą języka Java przy użyciu popularnych JMS interfejsu API i protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="f7002-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="f7002-197">Umożliwia także Service Bus protokołu AMQP 1.0 z innych języków, w tym .NET, C, Python i PHP.</span><span class="sxs-lookup"><span data-stu-id="f7002-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="f7002-198">Składniki utworzone przy użyciu tych języków można niezawodnie wymiany wiadomości i przy pełnej rozdzielczości, przy użyciu protokołu AMQP 1.0 obsługuje w usłudze Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f7002-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7002-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7002-199">Next steps</span></span>
* [<span data-ttu-id="f7002-200">Obsługa protokołu AMQP 1.0 w Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="f7002-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="f7002-201">Jak używać protokołu AMQP 1.0 z interfejsu API usługi Service Bus .NET</span><span class="sxs-lookup"><span data-stu-id="f7002-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="f7002-202">Service Bus protokołu AMQP 1.0 przewodnik dewelopera</span><span class="sxs-lookup"><span data-stu-id="f7002-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="f7002-203">Wprowadzenie do kolejek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="f7002-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="f7002-204">Centrum deweloperów języka Java</span><span class="sxs-lookup"><span data-stu-id="f7002-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

