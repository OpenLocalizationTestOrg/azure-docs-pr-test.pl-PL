---
title: "aaaHow toouse Azure Service Bus z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak zestaw SDK zadań Webjob hello toouse Azure Service Bus kolejek i tematów."
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
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>W jaki sposób toouse usługa Azure Service Bus z hello zestaw SDK zadań Webjob
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# jak przykłady kodu przedstawiające tootrigger proces po odebraniu wiadomości usługi Azure Service Bus. Przykłady kodu Hello użyj [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md).

wstawki kodu Hello Pokaż tylko funkcje, nie hello kod, który tworzy hello `JobHost` obiektu jak w poniższym przykładzie:

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

A [pełny przykład kodu usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) znajduje się w repozytorium azure-zadań webjob sdk przykłady hello w witrynie GitHub.com.

## <a id="prerequisites"></a>Wymagania wstępne
toowork usługi Service Bus oferuje tooinstall hello [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet pakietu dodatkowo toohello inne pakiety zestaw SDK zadań Webjob. 

Masz również parametry połączenia AzureWebJobsServiceBus hello tooset w parametry połączenia magazynu toohello dodanie.  Można to zrobić w hello `connectionStrings` sekcji hello pliku App.config, jak pokazano w hello poniższy przykład:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

Aby uzyskać przykładowy projekt, który zawiera ustawienie parametrów połączenia usługi Service Bus hello w pliku App.config hello, zobacz [przykład usługi Service Bus](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus). 

można również ustawić parametry połączenia Hello w hello środowiska uruchomieniowego platformy Azure, które następnie zastępują ustawienia App.config hello, po uruchomieniu hello zadania WebJob na platformie Azure; Aby uzyskać więcej informacji, zobacz [wprowadzenie hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).

## <a id="trigger"></a>Jak odebraniu tootrigger funkcja, gdy komunikat kolejki usługi Service Bus
wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello `ServiceBusTrigger` atrybutu. Konstruktor atrybutu Hello przyjmuje parametr określający nazwę hello hello toopoll kolejki.

### <a name="how-servicebustrigger-works"></a>Jak działa ServiceBusTrigger
Hello SDK odbiera komunikat w `PeekLock` tryb i wywołania `Complete` na wiadomość powitania, jeśli funkcja hello zakończy działanie pomyślnie, lub wywołania `Abandon` Jeśli funkcja hello nie powiedzie się. Jeśli funkcja hello uruchomione dłużej niż hello `PeekLock` limit czasu blokady hello jest automatycznie odnawiane.

Usługi Service Bus ma własną obsługi skażone kolejki, która nie może być kontrolowana ani konfigurowane za pomocą hello zestaw SDK zadań Webjob. 

### <a name="string-queue-message"></a>Ciąg komunikatu w kolejce
Witaj Poniższy przykładowy kod odczytuje komunikat z kolejki, zawiera ciąg, który zapisuje toohello ciąg hello zestaw SDK zadań Webjob pulpitu nawigacyjnego.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**Uwaga:** w przypadku tworzenia hello kolejki komunikatów w aplikacji, która nie używa hello zestaw SDK zadań Webjob, upewnij się, że tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) zbyt "text/plain".

### <a name="poco-queue-message"></a>Komunikat z kolejki POCO
Hello SDK zostanie automatycznie deserializacji komunikatu w kolejce, który zawiera dane JSON dla POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) typu. Witaj Poniższy przykładowy kod odczytuje komunikat z kolejki, która zawiera `BlobInformation` obiektu, który ma `BlobName` właściwości:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Aby uzyskać przykłady kodu przedstawiający sposób hello takie same właściwości toouse hello toowork POCO z obiektów blob i tabelach w funkcji, zobacz hello [wersji magazynu kolejek w tym artykule](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).

Jeśli swój kod, który tworzy komunikat z kolejki hello nie używa hello zestaw SDK zadań Webjob, należy użyć kodu toohello podobnie poniższy przykład:

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>Typy ServiceBusTrigger współpracuje z
Oprócz `string` i POCO typy, można użyć hello `ServiceBusTrigger` atrybut z tablicy bajtów lub `BrokeredMessage` obiektu.

## <a id="create"></a>Jak toocreate usługi Service Bus kolejki komunikatów
toowrite funkcję, która tworzy nowy komunikat kolejki użyć hello `ServiceBus` atrybutu i podaj hello kolejki nazwa toohello atrybut konstruktora. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>Utwórz pojedynczy komunikat z kolejki w funkcji z systemem innym niż async
powitania po przykładowy kod używa toocreate parametru wyjściowego nowej wiadomości w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello komunikat w kolejce hello o nazwie "inputqueue".

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

Parametr wyjściowy Hello tworzenia pojedynczy komunikat z kolejki mogą być następujące typy hello:

* `string`
* `byte[]`
* `BrokeredMessage`
* Można serializować typu POCO zdefiniowana. Automatycznie zserializowanym w formacie JSON.

Parametry typu POCO komunikatu w kolejce jest tworzony, gdy kończy się funkcja hello; Jeśli parametr hello ma wartość null, hello SDK tworzy komunikat z kolejki, który zwróci wartość null, podczas wiadomości powitania jest odbierany i deserializacji. Dla hello innych typów, jeśli parametr hello ma wartość null komunikatu w kolejce nie zostanie utworzony.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>Tworzenie wielu wiadomości w kolejce lub w funkcji asynchronicznych
toocreate wiele komunikatów, należy użyć hello `ServiceBus` atrybutem `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w powitania po przykładowym kodzie:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Każdy komunikat kolejki jest tworzony natychmiast po hello `Add` metoda jest wywoływana.

## <a id="topics"></a>Jak toowork z tematów usługi Service Bus
wywołuje funkcję hello SDK toowrite po odebraniu wiadomości na temat usługi Service Bus, użyj hello `ServiceBusTrigger` atrybut z konstruktora hello, który przyjmuje nazwy tematu i subskrypcji, jak pokazano w powitania po przykładowym kodzie:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

toocreate komunikat na temat użycia hello `ServiceBus` atrybutem hello nazwa tematu sam sposobu korzystania z kolejki.

## <a name="features-added-in-release-11"></a>Funkcje dodane w wersji 1.1
Witaj, następujące funkcje zostały dodane w wersji 1.1:

* Zezwalaj na możliwość głębokiego dostosowania przetwarzania za pośrednictwem komunikatu `ServiceBusConfiguration.MessagingProvider`.
* `MessagingProvider`Dostosowywanie hello usługi Service Bus obsługuje `MessagingFactory` i `NamespaceManager`.
* A `MessageProcessor` strategii wzorzec umożliwia toospecify procesora na kolejki/tematu.
* Współbieżność przetwarzania komunikatu jest obsługiwany przez domyślną. 
* Łatwe dostosowywanie `OnMessageOptions` za pośrednictwem `ServiceBusConfiguration.MessageOptions`.
* Zezwalaj na [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) toobe określone na `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (dla scenariuszy, w którym możesz nie mieć Zarządzanie prawami). Należy pamiętać, że zadań Webjob Azure tooautomatically nie można udostępnić nieistniejącą kolejek i tematów bez AccessRights zarządzania.

## <a id="queues"></a>Tematy pokrewne objętych hello magazynu kolejek jak tooarticle
Aby uzyskać informacje o scenariuszach zestaw SDK zadań Webjob nie dotyczą tooService magistrali, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy w tym artykule Uwzględnij hello następujące elementy:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
* Ustawianie parametrów połączenia SDK hello w kodzie
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z usługi Azure Service Bus. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

