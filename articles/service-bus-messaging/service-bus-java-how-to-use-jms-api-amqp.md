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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Jak toouse hello Java wiadomości usługi (JMS) interfejsu API z usługi Service Bus i protokołu AMQP 1.0
Hello zaawansowane komunikatów usługi kolejkowania wiadomości protokołu (AMQP) 1.0 jest wydajne, niezawodne i poziom przesyłania komunikatów protokołu służy toobuild niezawodne, i platform aplikacji do obsługi wiadomości.

Obsługa protokołu AMQP 1.0 w usłudze Service Bus oznacza, że można użyć hello usługi kolejkowania wiadomości i publikowania/subskrypcji obsługiwanych przez brokera obsługi komunikatów funkcje z zakresu od platformy przy użyciu protokołu binarnego wydajne. Ponadto można tworzyć aplikacje obejmuje składniki utworzony przy użyciu różnych języków, struktur i systemów operacyjnych.

W tym artykule opisano, jak toouse funkcji usługi Service Bus obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) z aplikacji języka Java przy użyciu hello protokół popularnych Java wiadomości usługi (JMS) w standardowe interfejsu API. Brak [artykułu Pomocnika](service-bus-amqp-dotnet.md) objaśniający sposób toodo hello tego samego, przy użyciu interfejsu API usługi Service Bus .NET hello. Możesz użyć tych toolearn razem dwa przewodniki dotyczące obsługi wielu platform wiadomości przy użyciu protokołu AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Rozpoczynanie pracy z usługą Service Bus
W tym przewodniku założono, że już przestrzeń nazw magistrali usług zawierający kolejki o nazwie **kolejki Kolejka1**. Jeśli nie chcesz, możesz [tworzenie przestrzeni nazw hello i kolejki](service-bus-create-namespace-portal.md) przy użyciu hello [portalu Azure](https://portal.azure.com). Aby uzyskać więcej informacji na temat sposobu przestrzeni nazw usługi Service Bus toocreate i kolejek, zobacz [Rozpoczynanie pracy z kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Partycjonowane kolejki i tematy obsługują także protokołu AMQP. Aby uzyskać więcej informacji, zobacz [partycjonowane jednostki do obsługi komunikatów](service-bus-partitioning.md) i [obsługi protokołu AMQP 1.0 dla usługi Service Bus podzielona na partycje, kolejek i tematów](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Biblioteka klienta protokołu AMQP 1.0 JMS hello pobierania
Informacje o którym toodownload hello najnowszej wersji biblioteki klienta hello Apache Qpid JMS protokołu AMQP 1.0, można znaleźć [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Należy dodać następujące cztery pliki JAR z hello Apache Qpid JMS protokołu AMQP 1.0 dystrybucji archiwum toohello klasy Java, podczas tworzenia i uruchamiania aplikacji JMS za pomocą usługi Service Bus hello:

* geronimo jms\_1.1\_1.0.jar specyfikacji
* qpid-amqp-1-0-Client-[Version].JAR
* qpid-amqp-1-0-Client-jms-[Version].JAR
* qpid-amqp-1-0-Common-[Version].JAR

## <a name="coding-java-applications"></a>Kodowanie aplikacji Java
### <a name="java-naming-and-directory-interface-jndi"></a>Nazewnictwo Java i katalog interfejsu (JNDI)
JMS używa hello nazywania Java i katalog interfejsu (JNDI) toocreate rozdzielenie nazwy logicznej i fizycznej. Dwa typy obiektów JMS są rozpoznawane przy użyciu JNDI: ConnectionFactory i docelowego. JNDI korzysta z modelu dostawcy, w którym można podłączyć innego katalogu usługi toohandle Nazwa rozwiązania obowiązków. Witaj Apache Qpid JMS protokołu AMQP 1.0 biblioteka zawiera proste właściwości opartych na plikach JNDI dostawcy, który jest skonfigurowany przy użyciu pliku właściwości hello następującego formatu:

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

#### <a name="configure-hello-connectionfactory"></a>Skonfiguruj hello ConnectionFactory
Witaj toodefine wpis **ConnectionFactory** w hello Qpid właściwości pliku JNDI dostawcy jest zgodny z formatem hello:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Gdzie **[jndi_name]** i **[ConnectionURL]** mają następujące znaczenie hello:

* **[jndi_name]** : hello nazwę logiczną hello ConnectionFactory. To jest nazwa hello zostaną rozwiązane w aplikacji Java hello przy użyciu metody JNDI IntialContext.lookup() hello.
* **[ConnectionURL]** : Adres URL, który dostarcza informacji hello hello JMS biblioteki wymagane toohello AMQP brokera.

Hello format hello **ConnectionURL** wygląda następująco:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Gdzie **[przestrzeń nazw]**, **[SASPolicyName]** i **[SASPolicyKey]** mają następujące znaczenie hello:

* **[przestrzeń nazw]** : hello przestrzeń nazw magistrali usług.
* **[SASPolicyName]** : Nazwa zasady hello sygnatura dostępu współdzielonego dla kolejki.
* **[SASPolicyKey]** : klucz zasad hello sygnatura dostępu współdzielonego dla kolejki.

> [!NOTE]
> Należy ręcznie hasła hello kodowania adresu URL. Przydatne narzędzie kodowania adresu URL jest dostępna na [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Konfigurowanie miejsc docelowych
wpis Hello używany toodefine jest obiektem docelowym jest hello Qpid właściwości pliku JNDI dostawcy hello następującego formatu:

```
queue.[jndi_name] = [physical_name]
```

lub

```
topic.[jndi_name] = [physical_name]
```

Gdzie **[jndi\_nazwę]** i **[fizycznych\_name]** mają następujące znaczenie hello:

* **[jndi_name]** : hello nazwy logicznej hello przeznaczenia. To jest nazwa hello zostaną rozwiązane w aplikacji Java hello przy użyciu metody JNDI IntialContext.lookup() hello.
* **[physical_name]** : Nazwa hello hello aplikacji hello toowhich jednostek usługi Service Bus wysłania lub odebrania wiadomości.

> [!NOTE]
> Podczas odbierania z subskrypcję tematu usługi Service Bus, hello nazwa fizycznego określony w JNDI powinna być nazwą hello hello tematu. Nazwa subskrypcji Hello podano po utworzeniu subskrypcji trwałe hello hello JMS kodu aplikacji. Witaj [Service Bus protokołu AMQP 1.0 przewodnik dewelopera](service-bus-amqp-dotnet.md) zawiera więcej szczegółowych informacji dotyczących pracy z tematów usługi Service Bus z JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Pisanie aplikacji JMS hello
Nie ma żadnych specjalnych interfejsów API lub opcje potrzebne podczas korzystania z usługi Service Bus JMS. Istnieje jednak kilka ograniczeń, które zostały omówione później. Podobnie jak w dowolnej aplikacji JMS powitania po pierwsze wymagane jest konfiguracji środowiska JNDI hello, w stanie tooresolve toobe **ConnectionFactory** i miejsc docelowych.

#### <a name="configure-hello-jndi-initialcontext"></a>Skonfiguruj hello JNDI InitialContext
Witaj JNDI środowisko jest skonfigurowane przez przekazanie do hello Konstruktor klasy javax.naming.InitialContext hello hashtable informacji o konfiguracji. Witaj dwóch wymaganych elementów w obiekcie hashtable hello są nazwa klasy hello hello początkowej fabryki kontekstu i hello adres URL dostawcy. Witaj poniższy kod pokazuje, jak tooconfigure hello JNDI środowiska toouse hello Qpid właściwości pliku JNDI dostawcy z plikiem właściwości o nazwie **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Prostą aplikację JMS przy użyciu kolejki usługi Service Bus
Witaj następujący przykład program wysyła kolejki usługi Service Bus tooa JMS TextMessages z nazwy logicznej JNDI hello kolejki i odbiera wiadomości powitania ponownie.

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

### <a name="run-hello-application"></a>Uruchamianie aplikacji hello
Uruchomienie aplikacji hello generuje dane wyjściowe w formie hello:

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

## <a name="cross-platform-messaging-between-jms-and-net"></a>Wysyłanie komunikatów między JMS i .NET wielu platform
W tym przewodniku pokazano, jak toosend i odbieranie wiadomości tooand z usługi Service Bus przy użyciu JMS. Jedną z kluczowych zalet protokołu AMQP 1.0 hello jest jednak możliwość toobe aplikacje zbudowane na podstawie składników zapisany w różnych językach, za pomocą wiadomości wymieniane niezawodne i w pełnej rozdzielczości.

Przy użyciu aplikacji JMS przykładowej hello opisane powyżej i podobnych aplikacji .NET z artykułu pomocnika, [przy użyciu usługi Service Bus z .NET z protokołu AMQP 1.0](service-bus-amqp-dotnet.md), mogą wymieniać komunikaty między .NET i Java. Przeczytaj ten artykuł, aby uzyskać więcej informacji o szczegóły hello wieloplatformowych wiadomości przy użyciu usługi Service Bus i protokołu AMQP 1.0.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET wiadomości:

* Uruchom hello .NET przykładowej aplikacji bez żadnych argumentów wiersza polecenia.
* Z argumentem wiersza polecenia "sendonly" hello, należy uruchomić hello Java przykładowej aplikacji. W tym trybie hello aplikacji nie będą otrzymywać wiadomości z kolejki hello tylko wysyła.
* Naciśnij klawisz **Enter** kilka razy w konsoli aplikacji Java hello, który spowoduje, że toobe wiadomości wysyłane.
* Te komunikaty są odbierane przez hello aplikacji .NET.

#### <a name="output-from-jms-application"></a>Dane wyjściowe aplikacji JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Dane wyjściowe aplikacji .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
tooJMS .NET toodemonstrate wiadomości:

* Z argumentem wiersza polecenia "sendonly" hello, należy uruchomić hello .NET przykładowej aplikacji. W tym trybie hello aplikacji nie będą otrzymywać wiadomości z kolejki hello tylko wysyła.
* Uruchom hello Java przykładowej aplikacji bez żadnych argumentów wiersza polecenia.
* Naciśnij klawisz **Enter** kilka razy w hello konsoli aplikacji .NET, który spowoduje, że toobe wiadomości wysyłane.
* Te komunikaty są odbierane przez hello aplikacji Java.

#### <a name="output-from-net-application"></a>Dane wyjściowe aplikacji .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Dane wyjściowe aplikacji JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Nieobsługiwane funkcje i ograniczenia
Podczas przy użyciu JMS za pośrednictwem protokołu AMQP 1.0 z usługą Service Bus, a mianowicie istnieją Hello następujące ograniczenia:

* Tylko jeden **MessageProducer** lub **MessageConsumer** dozwolone jest używanie **sesji**. Jeśli potrzebujesz toocreate wiele **MessageProducers** lub **MessageConsumers** w aplikacji, Utwórz dedykowana **sesji** dla każdego z nich.
* Subskrypcje tematu nietrwałe nie są obecnie obsługiwane.
* **MessageSelectors** nie są obecnie obsługiwane.
* Tymczasowe miejsc docelowych; na przykład **TemporaryQueue**, **TemporaryTopic** nie są obecnie obsługiwane, wraz z hello **QueueRequestor** i **TopicRequestor**Interfejsów API, które z nich korzystają.
* Transakcyjne sesji i transakcje rozproszone nie są obsługiwane.

## <a name="summary"></a>Podsumowanie
Ten temat tooguide pokazano, jak toouse funkcji usługi Service Bus obsługiwanych przez brokera obsługi komunikatów (kolejki i publikowania/subskrypcji tematy) z języka Java przy użyciu hello popularnych JMS interfejsu API i protokołu AMQP 1.0.

Umożliwia także Service Bus protokołu AMQP 1.0 z innych języków, w tym .NET, C, Python i PHP. Składniki utworzone przy użyciu tych języków mogą wymieniać komunikaty, niezawodne i w pełnej rozdzielczości, przy użyciu obsługi hello protokołu AMQP 1.0 w usłudze Service Bus.

## <a name="next-steps"></a>Następne kroki
* [Obsługa protokołu AMQP 1.0 w Azure Service Bus](service-bus-amqp-overview.md)
* [Jak toouse protokołu AMQP 1.0 z hello interfejsu API usługi Service Bus .NET](service-bus-dotnet-advanced-message-queuing.md)
* [Service Bus protokołu AMQP 1.0 przewodnik dewelopera](service-bus-amqp-dotnet.md)
* [Wprowadzenie do kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/)

