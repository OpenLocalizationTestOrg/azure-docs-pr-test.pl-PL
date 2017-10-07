---
title: aaaOptimizing kodu platformy Azure w programie Visual Studio | Dokumentacja firmy Microsoft
description: "Informacje dotyczące sposobu Azure kodu optymalizacji narzędzia w programie Visual Studio sprawić, że kod bardziej niezawodny i lepszego wykonywania."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Optymalizacja kodu platformy Azure
W przypadku programowania aplikacji, które używają programu Microsoft Azure, istnieją pewne praktyk kodowania, należy wykonać toohelp uniknąć problemów z aplikacji, skalowalność, zachowania i wydajności w środowisku chmury. Firma Microsoft udostępnia narzędzia do analizy kodu platformy Azure, która rozpoznaje i identyfikuje niektóre z tych często napotkał problemy i ułatwia ich rozwiązywania. Możesz pobrać narzędzie hello w programie Visual Studio za pośrednictwem pakietu NuGet.

## <a name="azure-code-analysis-rules"></a>Azure reguł analizy kodu
Narzędzie do analizy kodu Azure Hello używa hello reguły tooautomatically Flaga Azure kodu, gdy znajdzie znanych problemów wpływających na wydajność. Wykryto problemy występują jako ostrzeżenia lub błędy kompilatora. Kod poprawki lub sugestie tooresolve hello ostrzeżenia lub błędu często są realizowane za pośrednictwem ikoną żarówki.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Unikaj używania domyślny tryb stanu sesji (w trakcie)
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Opis
Jeśli używasz tryb stanu sesji (w trakcie) domyślnego powitania dla aplikacji w chmurze, zostaną utracone stanu sesji.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Domyślnie tryb stanu sesji hello określone w pliku web.config hello jest w trakcie. Ponadto jeśli żadnego wpisu określony w pliku konfiguracji hello, tryb stanu sesji hello domyślnie tooin procesu. Witaj w trakcie tryb zapisuje stan sesji w pamięci na powitania serwera sieci web. Po uruchomieniu wystąpienia lub nowe wystąpienie jest używana do równoważenia obciążenia lub obsługi trybu failover, stan sesji hello przechowywane w pamięci na serwerze sieci web hello nie są zapisywane. Taka sytuacja uniemożliwia aplikacji hello jest skalowalna na powitania chmury.

Stan sesji ASP.NET obsługuje kilka opcji innego magazynu dla danych stanu sesji: InProc, StateServer, SQLServer, niestandardowe i Off. Zaleca się używanie niestandardowy tryb toohost danych w zewnętrznym sklepie stanu sesji, takie jak [dostawcę stanu sesji Azure Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Rozwiązanie
Jedno rozwiązanie zalecane jest toostore stanu sesji na usługi zarządzana pamięć podręczna. Dowiedz się, jak toouse [dostawcę stanu sesji Azure Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore Twojego stanu sesji. Użytkownik może również magazynu sesji stanu w innych miejscach tooensure się, że aplikacja jest skalowalna na powitania chmury. więcej informacji na temat rozwiązań alternatywnych, przeczytaj toolearn [trybów stanu sesji](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>Uruchom metody nie powinna być asynchroniczne
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Opis
Tworzenie metod asynchronicznych (takich jak [await](https://msdn.microsoft.com/library/hh156528.aspx)) poza hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody, a następnie wywołań metod asynchronicznych hello z [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Deklarowanie hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda async powoduje, że proces roboczy hello tooenter roli pętli ponownego uruchomienia.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Wywołanie metod asynchronicznych wewnątrz hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda powoduje roli procesu roboczego hello toorecycle środowiska uruchomieniowego hello chmury usługi. Podczas uruchamiania roli proces roboczy, wszystkie wykonywania programu ma miejsce w obrębie hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody. Witaj istniejącym [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) — metoda powoduje, że proces roboczy hello toorestart roli. Gdy środowiska uruchomieniowego roli procesu roboczego hello trafi hello metoda asynchroniczna, wywołuje wszystkie operacje po metodzie asynchronicznej hello, a następnie zwraca. Powoduje to, że proces roboczy hello tooexit roli z hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) — metoda i uruchom ponownie. W następnej iteracji hello wykonywania roli procesu roboczego hello trafień ponownie metody asynchronicznej hello i ponowne uruchomienia, powoduje także ponownie toorecycle roli procesu roboczego hello.

### <a name="solution"></a>Rozwiązanie
Umieść wszystkie operacje asynchroniczne poza hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody. Wywoływać metody asynchronicznej hello refaktoryzowane z wewnątrz hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody, takiej jak RunAsync .wait (). Narzędzie do analizy kodu Azure Hello może pomóc rozwiązać ten problem.

powitania po fragment kodu przedstawia hello kodu poprawkę dotyczącą tego problemu:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Sygnatura dostępu współdzielonego magistrali usługi uwierzytelniania
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Opis
Dostęp do sygnatury dostępu Współdzielonego jest używany do uwierzytelniania. Usługi kontroli dostępu (ACS) jest przestarzałe uwierzytelniania magistrali usługi.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Aby zwiększyć bezpieczeństwo Azure Active Directory zastępuje ACS uwierzytelniania przy użyciu uwierzytelniania sygnatury dostępu Współdzielonego. Zobacz [usługi Azure Active Directory jest hello przyszłych usług ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) informacji na powitania planu migracji.

### <a name="solution"></a>Rozwiązanie
Korzystanie z uwierzytelniania sygnatury dostępu Współdzielonego w aplikacjach. Witaj poniższy przykład pokazuje, jak toouse istniejących tooaccess tokenu sygnatury dostępu Współdzielonego usługi magistrali przestrzeni nazw lub jednostki.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Zobacz hello następujące tematy, aby uzyskać więcej informacji.

* Aby uzyskać ogólne informacje, zobacz [uwierzytelniania podpisu dostępu udostępnionych za pomocą usługi Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)
* [Jak toouse uwierzytelniania podpisu dostępu do udostępnionych z usługą Service Bus](https://msdn.microsoft.com/library/dn205161.aspx)
* Aby uzyskać przykładowy projekt, zobacz [uwierzytelniania przy użyciu dostępu sygnatury dostępu Współdzielonego z subskrypcji magistrali usług](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Należy rozważyć użycie tooavoid metody OnMessage "pętlę odbierania"
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Opis
tooavoid, przechodząc do "otrzymywać pętli" hello wywoływania **OnMessage** metoda jest lepszym rozwiązaniem do odbierania wiadomości niż hello wywoływania **Receive** — metoda. Jednak jeśli musisz użyć hello **Receive** metoda i określ serwer z systemem innym niż domyślny czas oczekiwania, upewnij się, czas oczekiwania serwera hello jest więcej niż jednej minuty.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Podczas wywoływania metody **OnMessage**, powitania klienta uruchamia pompę wewnętrzny komunikat, który sonduje stale kolejki hello lub subskrypcji. To przekazywanie komunikatów zawiera nieskończoną pętlę, która wystawia wywołanie tooreceive wiadomości. Jeśli upłynie limit czasu wywołania hello, wystawia nowe połączenie. Witaj — interwał limitu czasu jest określany przez wartość hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) właściwości hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)który jest używany.

Witaj zaletą używania **OnMessage** porównaniu zbyt**Receive** jest, że użytkownicy nie mają toomanually sondować komunikatów, obsługa wyjątków przetwarzać wiele komunikatów równolegle i ukończyć powitalnych komunikaty.

Jeśli należy wywołać **Receive** bez użycia wartość domyślną, należy się hello *ServerWaitTime* wartość jest więcej niż jednej minuty. Ustawienie *ServerWaitTime* toomore niż minuta uniemożliwia limit czasu, zanim pełni odbioru wiadomości powitania powitania serwera.

### <a name="solution"></a>Rozwiązanie
Zobacz hello następujące przykłady kodu dla zalecane użycia. Aby uzyskać więcej informacji, zobacz [QueueClient.OnMessage — metoda (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)i [QueueClient.Receive — metoda (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

wydajność hello tooimprove hello Azure infrastruktury obsługi wiadomości, zobacz wzorca projektowego hello [asynchroniczne Elementarz wiadomości](https://msdn.microsoft.com/library/dn589781.aspx).

Witaj poniżej przedstawiono przykład użycia **OnMessage** tooreceive wiadomości.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Witaj poniżej przedstawiono przykład użycia **Receive** czas oczekiwania, hello domyślnego serwera.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Witaj poniżej przedstawiono przykład użycia **Receive** z serwerem z systemem innym niż domyślny czas oczekiwania.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Należy rozważyć użycie metod asynchronicznych usługi Service Bus
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Opis
Za pomocą asynchroniczne wydajności tooimprove metod usługi Service Bus obsługiwanych przez brokera obsługi komunikatów.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Używanie metod asynchronicznych umożliwia współbieżności program aplikacji, ponieważ wykonywania każdego wywołania nie blokuje hello głównego wątku. Korzystając z usługi Service Bus metod do obsługi komunikatów, wykonywania operacji (wysyłanie, odbierania, usuwanie, itp.) jest czasochłonne. Teraz obejmuje hello przetwarzania operacji hello przez hello usługi Service Bus opóźnienia toohello dodanie hello żądania i odpowiedzi hello. tooincrease hello liczbę operacji na czas, operacji musi być wykonywany współbieżnie. Aby uzyskać więcej informacji można znaleźć zbyt[najlepsze rozwiązania dotyczące wydajności ulepszenia przy użyciu usługi magistrali obsługiwanych przez brokera obsługi komunikatów](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Rozwiązanie
Zobacz [QueueClient klasy (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) uzyskać informacji na temat sposobu toouse hello zalecane metody asynchronicznej.

wydajność hello tooimprove hello Azure infrastruktury obsługi wiadomości, zobacz wzorca projektowego hello [asynchroniczne Elementarz wiadomości](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Należy wziąć pod uwagę partycjonowania tematów i kolejek usługi Service Bus
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Opis
Partycji usługi Service Bus kolejek i tematów w celu poprawy wydajności z komunikatów usługi Service Bus.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Partycjonowanie tematów i kolejek usługi Service Bus zwiększa dostępność przepływności i usługi wydajności, ponieważ hello ogólną przepustowość partycjonowanej kolejka lub temat nie jest już ograniczone przez wydajności hello brokera komunikatów pojedynczego lub magazynie obsługi komunikatów. Ponadto tymczasowego awaria magazynie obsługi komunikatów nie należy partycjonowanej kolejka lub temat niedostępny. Aby uzyskać więcej informacji, zobacz [partycjonowania jednostek obsługi komunikatów](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Rozwiązanie
Witaj następującego kodu fragment kodu przedstawia sposób toopartition jednostki do obsługi komunikatów.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Aby uzyskać więcej informacji, zobacz [podzielona na partycje kolejek usługi Service Bus i tematy | Blog usługi Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) i wyewidencjonowania hello [Microsoft Azure na partycje kolejką usługi Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) próbki.

## <a name="do-not-set-sharedaccessstarttime"></a>Nie ustawiaj SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Opis
Należy unikać używania SharedAccessStartTimeset toohello bieżącym uruchomieniu tooimmediately hello zasad dostępu udostępnionego. Wystarczy tooset tej właściwości Jeśli zasady dostępu udostępnionego hello toostart w późniejszym czasie.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Synchronizacja zegara powoduje, że czas niewielkie różnice centrów danych. Na przykład można logicznie się spodziewać czas rozpoczęcia hello ustawienia magazynu zasad sygnatury dostępu Współdzielonego jako hello bieżący czas za pomocą DateTime.Now lub podobnej metody spowoduje, że hello SAS zasad tootake obowiązywać natychmiast. Jednak hello czasu niewielkie różnice między centrami danych może spowodować problemy z tym, ponieważ sytuacje centrum danych mogą być nieco później niż czas rozpoczęcia hello, podczas gdy inne wcześniejsze go. W związku z tym hello SAS zasad można wygaśnie szybko (lub nawet natychmiast) Jeśli okres istnienia zasad hello jest zbyt krótki.

Aby uzyskać więcej pomocy na temat używania sygnatura dostępu współdzielonego w magazynie Azure, zobacz [wprowadzenie tabeli SAS (Shared Access Signature), SAS kolejki i tooBlob aktualizacji SAS - Microsoft Azure Blog zespołu usługi Magazyn — strona główna — lokacji blogi MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Rozwiązanie
Usuń hello instrukcja, która ustawia czas rozpoczęcia hello hello udostępnionych zasad dostępu. Narzędzie do analizy kodu Azure Hello przedstawiono rozwiązanie tego problemu. Aby uzyskać więcej informacji dotyczących zarządzania zabezpieczeniami, zobacz wzorca projektowego hello [wzorzec klucza Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Witaj następującego fragmentu kodu pokazuje hello kodu poprawkę dotyczącą tego problemu.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Udostępnione czas wygaśnięcia musi być przeprowadzona ponad pięć minut zasad dostępu
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Opis
Może istnieć jak pięciu minut różnica w zegary między centrami danych w różnych lokalizacjach powodu warunku tooa znana jako "przesunięcia czasowego zegara." tooprevent hello SAS zasady wygaśnięcia wcześniej niż ustawić token toobe czas wygaśnięcia hello więcej niż pięć minut.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Synchronizuj centrów danych w różnych miejscach na całym świecie hello sygnał zegara. Ponieważ czas dla lokalizacji toodifferent tootravel sygnał zegara, może istnieć wariancji czas między centrami danych w różnych lokalizacjach geograficznych mimo wszystko, co prawdopodobnie jest zsynchronizowany. Ta różnica czasu może mieć wpływ na powitania dostęp współdzielony początkowy czas i wygaśnięcia interwał zasad. W związku z tym tooensure zasad udostępnionych dostępu ma efekt natychmiastowy, nie podaje godziny rozpoczęcia hello. Ponadto upewnij się, że czas wygaśnięcia hello jest większa niż 5 minut tooprevent wczesne przekroczenia limitu czasu.

Aby uzyskać więcej informacji o korzystaniu z sygnaturą dostępu współdzielonego w magazynie Azure, zobacz [wprowadzenie tabeli SAS (Shared Access Signature), SAS kolejki i tooBlob aktualizacji SAS - Microsoft Azure Blog zespołu usługi Magazyn — strona główna — lokacji blogi MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Rozwiązanie
Aby uzyskać więcej informacji dotyczących zarządzania zabezpieczeniami, zobacz wzorca projektowego hello [wzorzec klucza Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Hello poniżej znajduje się przykład nieokreślenie godzinę rozpoczęcia zasad dostępu udostępnionego.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Witaj poniżej znajduje się przykład określenia godziny rozpoczęcia zasad dostęp współdzielony z okresem ważności zasady więcej niż pięć minut.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Aby uzyskać więcej informacji, zobacz [tworzenia i używania sygnaturę dostępu współdzielonego](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Użyj CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Opis
Przy użyciu hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) klasy dla projektów, takie jak witryny sieci Web Azure i usług Azure mobile services nie będzie powodować problemy środowiska wykonawczego. Najlepszym rozwiązaniem jest jednak dobrze toouse chmury[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) jako jednolity sposób zarządzania konfiguracjami dla wszystkich aplikacji w chmurze Azure.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
CloudConfigurationManager odczytuje hello konfiguracji pliku właściwe toohello aplikacji środowiska.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Rozwiązanie
Refaktoryzuj hello toouse Twojego kodu [klasa CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Kod poprawkę dotyczącą tego problemu są udostępniane przez narzędzie do analizy kodu Azure hello.

Witaj następującego fragmentu kodu pokazuje hello kodu poprawkę dotyczącą tego problemu. Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

Z

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Poniżej przedstawiono przykład sposobu toostore hello ustawienie konfiguracji w pliku App.config lub Web.config. Dodaj hello ustawienia toohello sekcji appSettings pliku konfiguracji hello. Oto Hello hello pliku Web.config dla hello poprzednim przykładzie kodu.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Unikaj używania ciągów połączenia stałe
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Opis
Jeśli używasz parametry połączenia ustalony i trzeba tooupdate je później, należy mieć kod źródłowy tooyour zmiany toomake i ponowne skompilowanie aplikacji hello. Jednak jeśli parametry połączenia są przechowywane w pliku konfiguracji, można zmienić je później, po prostu aktualizując hello pliku konfiguracji.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Koduj parametrów połączenia jest zła rozwiązaniem, ponieważ wprowadza ona problemów, jeśli parametry połączenia muszą toobe szybko zmienić. Ponadto jeśli hello projektu musi toobe zaznaczone w formancie toosource, parametry połączenia ustalony wprowadzić luk w zabezpieczeniach, ponieważ ciągi hello można wyświetlić w kodzie źródłowym hello.

### <a name="solution"></a>Rozwiązanie
Przechowywanie parametrów połączenia w plikach konfiguracji hello lub środowisk Azure.

* Dla aplikacji autonomicznej należy użyć ustawień parametrów połączenia toostore app.config.
* Dla aplikacji hostowanych przez usługi IIS sieci web Użyj parametrów połączenia toostore pliku web.config.
* Dla aplikacji vNext ASP.NET Użyj parametrów połączenia toostore configuration.json.

Informacje na temat używania plików konfiguracji, takich jak plik web.config lub app.config, zobacz [wskazówki dotyczące konfigurowania sieci Web ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Uzyskać informacji na temat sposobu Azure pracy zmiennych środowiska, zobacz [Azure Web Sites: jak ciągi aplikacji i działać ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Aby uzyskać informacje na przechowywanie parametrów połączenia w kontroli źródła, zobacz [należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytorium kodu źródłowego](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Użyj pliku konfiguracji diagnostyki
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Opis
Zamiast konfigurować ustawienia diagnostyki w kodzie, takich jak przy użyciu hello Microsoft.WindowsAzure.Diagnostics programowania interfejsu API, należy skonfigurować ustawienia diagnostyki w pliku diagnostics.wadcfg hello. (Lub diagnostics.wadcfgx, jeśli używasz 2.5 zestawu SDK platformy Azure). W ten sposób można zmienić ustawień diagnostycznych bez konieczności toorecompile kodu.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Przed 2.5 zestawu SDK platformy Azure, (używający Diagnostyka Azure 1.3), Azure Diagnostics (WAD) może zostać skonfigurowany przy użyciu kilka różnych metod: dodanie go toohello konfiguracji blob w magazynie, za pomocą kodu konieczne, deklaratywne konfiguracji lub hello domyślne Konfiguracja. Jednak hello preferowane toouse plik konfiguracyjny XML (diagnostics.wadcfg lub diagnositcs.wadcfgx dla zestawu SDK, 2.5 i nowszych) w projekcie aplikacji hello jest sposób tooconfigure diagnostyki. W takie podejście plik diagnostics.wadcfg hello całkowicie definiuje konfigurację hello i aktualizowanie i wdrożone w momencie. Mieszanie hello użycie pliku konfiguracji diagnostics.wadcfg hello z hello metod programistycznych ustawienia konfiguracji za pomocą hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)lub [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) klas może prowadzić tooconfusion. Zobacz [zainicjować lub zmienianie konfiguracji diagnostyki Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) Aby uzyskać więcej informacji.

Począwszy od 1.3 WAD (dołączony do 2.5 zestawu SDK platformy Azure), nie jest już możliwe toouse kodu tooconfigure diagnostyki. W związku z tym można podać tylko konfiguracji hello podczas stosowania lub aktualizowania hello diagnostyki rozszerzenia.

### <a name="solution"></a>Rozwiązanie
Użyj hello diagnostyki toomove projektanta ustawień diagnostycznych toohello diagnostyki konfiguracji pliku konfiguracji (diagnositcs.wadcfg lub diagnositcs.wadcfgx dla zestawu SDK, 2.5 i nowszych). Zaleca się zainstalowanie [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) i korzystać z najnowszych funkcji diagnostyki hello.

1. W menu skrótów hello hello roli, które mają tooconfigure wybierz polecenie Właściwości, a następnie wybierz kartę Konfiguracja hello.
2. W hello **diagnostyki** sekcji, upewnij się, że hello **włączyć diagnostyki** pole wyboru jest zaznaczone.
3. Wybierz hello **Konfiguruj** przycisku.

   ![Dostęp do opcji Włącz diagnostyki hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Zobacz [Konfigurowanie diagnostyki dla usług Azure Cloud Services i maszyn wirtualnych](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) Aby uzyskać więcej informacji.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Unikaj deklarowanie obiektów DbContext jako statyczne
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Opis
pamięć toosave uniknąć deklarowanie obiektów DBContext jako statyczny.

Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Przyczyna
Obiekty DBContext przechowują hello wyników zapytania z każdym wywołaniu. Obiekty DBContext statyczne nie są usuwane, dopóki nie zostanie zwolniony hello domeny aplikacji. W związku z tym statycznego obiektu DBContext może używać dużych ilości pamięci.

### <a name="solution"></a>Rozwiązanie
Zadeklarować zmiennej lokalnej lub pole wystąpienia niestatycznego DBContext, użyj go zadania, a następnie pozwól mu usuwane po użyciu.

Hello następujące klasy kontrolera MVC przykładzie pokazano, jak toouse hello obiektu DBContext.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat optymalizacji i rozwiązywanie problemów z aplikacjami platformy Azure, zobacz [Rozwiązywanie problemów aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
