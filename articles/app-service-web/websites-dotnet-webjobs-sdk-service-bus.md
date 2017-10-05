---
title: "Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs"
description: "Dowiedz się, jak używać tematów i kolejek usługi Azure Service Bus przy użyciu zestawu SDK zadań Webjob."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a>Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# przykłady kodu, których pokazano, jak do wyzwalania procesu po odebraniu wiadomości usługi Azure Service Bus. Kod przykłady użycia [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md).

Wstawki kodu Pokaż tylko funkcje, nie tworzy kodu `JobHost` obiektu jak w poniższym przykładzie:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

A [pełny przykład kodu usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) znajduje się w repozytorium azure-zadań webjob sdk próbek w witrynie GitHub.com.

## <a id="prerequisites"></a>Wymagania wstępne
Do pracy z usługą Service Bus, musisz zainstalować [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) pakietu NuGet, oprócz innych pakietów zestaw SDK zadań Webjob. 

Należy również ustawić parametry połączenia AzureWebJobsServiceBus oprócz parametry połączenia magazynu.  Można to zrobić w `connectionStrings` sekcji w pliku App.config, jak pokazano w poniższym przykładzie:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Aby uzyskać przykładowy projekt, który zawiera ustawienie parametrów połączenia magistrali usług w pliku App.config, zobacz [przykład usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

Można również ustawić parametry połączenia w środowisko uruchomieniowe platformy Azure, które następnie zastępują ustawienia App.config, po uruchomieniu zadania WebJob na platformie Azure; Aby uzyskać więcej informacji, zobacz [wprowadzenie do zestawu SDK WebJobs](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Sposób włączania funkcji po odebraniu komunikatu w kolejce usługi Service Bus
Aby napisać funkcję, która wywołuje zestaw SDK zadań Webjob po odebraniu komunikatu w kolejce, użyj `ServiceBusTrigger` atrybutu. Konstruktor atrybutu ma parametr, który określa nazwę kolejki do sondowania.

### <a name="how-servicebustrigger-works"></a>Jak działa ServiceBusTrigger
Zestaw SDK odbiera wiadomości w `PeekLock` tryb i wywołania `Complete` na komunikat, jeśli funkcja zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli funkcja nie powiedzie się. Jeśli funkcja uruchomione dłużej niż `PeekLock` limit czasu blokady automatycznie zostanie odnowiona.

Usługi Service Bus ma własną obsługi skażone kolejki, która nie może być kontrolowana ani skonfigurowane przez zestaw SDK zadań Webjob. 

### <a name="string-queue-message"></a>Ciąg komunikatu w kolejce
Poniższy przykładowy kod odczytuje komunikat z kolejki, który zawiera ciąg i zapisuje ciąg do pulpitu nawigacyjnego, zestaw SDK zadań Webjob.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Uwaga:** wiadomości w kolejce w przypadku tworzenia w aplikacji, która nie korzysta z zestawu SDK zadań Webjob, upewnij się ustawić [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) do "text/plain".

### <a name="poco-queue-message"></a>Komunikat z kolejki POCO
Zestaw SDK zostanie automatycznie deserializacji komunikatu w kolejce, który zawiera dane JSON dla POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) typu. Poniższy przykładowy kod odczytuje komunikat z kolejki, która zawiera `BlobInformation` obiektu, który ma `BlobName` właściwości:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

Dla przykładów kodu przedstawiający sposób użycia właściwości POCO do pracy z obiektów blob i tabelach w tej samej funkcji, zobacz [wersji magazynu kolejek w tym artykule](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Jeśli zestaw SDK zadań Webjob nie są używane swój kod, który tworzy komunikat z kolejki, należy użyć kodu podobne do poniższego przykładu:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Typy ServiceBusTrigger współpracuje z
Oprócz `string` i POCO typy, można użyć `ServiceBusTrigger` atrybut z tablicy bajtów lub `BrokeredMessage` obiektu.

## <a id="create"></a>Jak utworzyć wiadomości do kolejki usługi Service Bus
Aby napisać funkcję, która tworzy nowy Użyj komunikat kolejki `ServiceBus` atrybutu i przekaż nazwę kolejki do konstruktora atrybutów. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Utwórz pojedynczy komunikat z kolejki w funkcji z systemem innym niż async
Poniższy przykładowy kod używa parametru wyjściowego można utworzyć nowej wiadomości w kolejce o nazwie "outputqueue" o tej samej zawartości, co komunikat w kolejce o nazwie "inputqueue".

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

Parametr wyjściowy do tworzenia pojedynczy komunikat z kolejki może być dowolny z następujących typów:

* `string`
* `byte[]`
* `BrokeredMessage`
* Można serializować typu POCO zdefiniowana. Automatycznie zserializowanym w formacie JSON.

Parametry typu POCO komunikatu w kolejce jest tworzony, gdy kończy się funkcja; Jeśli parametr ma wartość null, zestaw SDK tworzy komunikat z kolejki, która zwróci wartość null, gdy komunikat jest odbierany i deserializacji. Dla innych typów Jeśli parametr ma wartość null komunikatu w kolejce nie zostanie utworzony.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Tworzenie wielu wiadomości w kolejce lub w funkcji asynchronicznych
Aby utworzyć wiele komunikatów, użyj `ServiceBus` atrybutem `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w poniższym przykładzie kodu:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Każdy komunikat kolejki jest tworzony natychmiast po `Add` metoda jest wywoływana.

## <a id="topics"></a>Jak pracować z tematów usługi Service Bus
Aby napisać funkcję, która wywołuje zestawu SDK, gdy wiadomość zostanie odebrana na temat usługi Service Bus, użyj `ServiceBusTrigger` atrybut z konstruktora, który przyjmuje nazwy tematu i subskrypcji, jak pokazano w poniższym przykładzie kodu:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

Aby utworzyć komunikat na temat, użyj `ServiceBus` atrybutu o nazwie tematu taki sam sposób korzystasz z kolejki.

## <a name="features-added-in-release-11"></a>Funkcje dodane w wersji 1.1
Następujące funkcje zostały dodane w wersji 1.1:

* Zezwalaj na możliwość głębokiego dostosowania przetwarzania za pośrednictwem komunikatu `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`Dostosowywanie usługi Service Bus obsługuje `MessagingFactory` i `NamespaceManager`.
* A `MessageProcessor` wzorzec strategii pozwala na określenie procesora na kolejki/tematu.
* Współbieżność przetwarzania komunikatu jest obsługiwany przez domyślną. 
* Łatwe dostosowywanie `OnMessageOptions` za pośrednictwem `ServiceBusConfiguration.MessageOptions`.
* Zezwalaj na [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) podane na `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (dla scenariuszy, w którym możesz nie mieć Zarządzanie prawami). Należy pamiętać, że zadań Webjob Azure nie można automatycznie udostępnić nieistniejącej kolejki i tematy bez AccessRights zarządzania.

## <a id="queues"></a>Tematy pokrewne objętych artykułem porad kolejki magazynu
Aby uzyskać informacje o scenariuszach zestaw SDK zadań Webjob nie specyficzne dla usługi Service Bus, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy w tym artykule są następujące:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji
* Ustaw parametry połączenia SDK w kodzie
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
Ten przewodnik zawiera podane przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z usługi Azure Service Bus. Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

