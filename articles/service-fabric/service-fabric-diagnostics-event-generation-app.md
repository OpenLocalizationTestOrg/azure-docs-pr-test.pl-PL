---
title: "aaaAzure monitorowania poziomu aplikacji usługi sieci szkieletowej | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o aplikacji i zdarzenia dotyczące poziomu usług i dzienniki używane toomonitor i diagnozowanie klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>Generowanie zdarzeń i dzienników na poziomie aplikacji i usług

## <a name="instrumenting-hello-code-with-custom-events"></a>Kod Instrumentacji hello zdarzeń niestandardowych

Instrumentacja hello kod stanowi podstawę hello najbardziej inne aspekty monitorowania usług. Instrumentacja jest jedynym sposobem hello, które można określić, że dany element jest nieprawidłowy i toodiagnose, co wymaga toobe stałej. Chociaż jest technicznie możliwe tooconnect usługi produkcji tooa debugera, nie jest typowym rozwiązaniem. Tak o szczegółowe dane Instrumentacji jest ważna.

Niektóre produkty automatyczną Instrumentację kodu. Mimo że te rozwiązania mogą również działać, ręczne Instrumentacja prawie zawsze jest wymagana. W celu hello musi mieć wystarczającą ilość tooforensically informacji debugowania aplikacji hello. W tym dokumencie opisano różne podejścia tooinstrumenting kodu, i gdy toochoose jednej metody zamiast innego.

## <a name="eventsource"></a>Źródła zdarzeń
Po utworzeniu rozwiązania sieci szkieletowej usług z szablonu w programie Visual Studio, **EventSource**-klasy (**ServiceEventSource** lub **ActorEventSource**) jest generowany. Utworzyć szablonu, w którym można dodać zdarzeń dla usługi lub aplikacji. Witaj **EventSource** nazwa **musi** być unikatowa i powinny zostać zmienione z ciąg szablonu domyślnego hello Moja firma -&lt;rozwiązania&gt; - &lt; Projekt&gt;. Istnieniem wielu **EventSource** definicje, które używają hello tej samej przyczyny nazwa problem w czasie wykonywania. Każdy zdefiniowane zdarzenie musi mieć unikatowy identyfikator. Jeśli identyfikator nie jest unikatowa, wystąpi błąd czasu wykonywania. Niektóre organizacje preassign zakresów wartości dla identyfikatorów tooavoid konfliktów między oddzielne zespoły deweloperów. Aby uzyskać więcej informacji, zobacz [zaliczko w blogu](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) lub hello [dokumentacji MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>W przypadku używania strukturalnych zdarzeń źródła zdarzeń

Każdego zdarzenia hello w hello przykłady kodu w tej sekcji są definiowane dla określonych przypadków, na przykład podczas rejestrowania typu usługi. Podczas definiowania wiadomości w przypadku użycia, danych można spakować z tekstem hello hello błędu i można więcej łatwo wyszukiwać i filtr na podstawie nazwy hello lub wartości hello określonej właściwości. Struktury wyjście Instrumentacji hello umożliwia łatwiejsze tooconsume, ale wymaga więcej myśl i godziny toodefine nowe zdarzenie dla każdego przypadku użycia. Definicje zdarzeń mogą być współużytkowane przez hello całej aplikacji. Na przykład metoda uruchamiania lub zatrzymywania zdarzeń będzie można używać ponownie w wielu usług w aplikacji. Usługa specyficznego dla domeny, takich jak system zamówień może mieć **CreateOrder** zdarzenie, które ma własną unikatową zdarzeń. Takie podejście może wygenerować wiele zdarzeń i mogą wymagać koordynacji identyfikatorów zespołów projektu. 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>Ogólnie przy użyciu źródła zdarzeń

Definiowanie określonych zdarzeń mogą być trudne, wiele osób zdefiniować kilka zdarzenia ze wspólnego zestawu parametrów, które zwykle wysyłają informacji o ich jako ciąg. Większość aspekt hello strukturę zostaną utracone i jest trudniej toosearch i filtrować wyniki hello. W takie podejście kilka zdarzeń, które zwykle odpowiadają poziomy rejestrowania toohello są zdefiniowane. Witaj następującego fragmentu definiuje debugowania i komunikatu o błędzie:

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

Przy użyciu hybrydowego Instrumentacji strukturalnych i rodzajowy również może działać również. Strukturalne Instrumentacji jest używana do raportowania błędów i metryki. Zdarzenia ogólne może służyć do hello szczegółowe rejestrowanie, który jest używane przez inżynierów do rozwiązywania problemów.

## <a name="aspnet-core-logging"></a>Platformy ASP.NET Core rejestrowania

Toocarefully ważne jego Zaplanuj, jak będzie Instrumentacja kodu. plan prawym Instrumentacji Hello może pomóc w uniknięciu potencjalnie destabilizing bazy kodu, a następnie konieczności tooreinstrument hello kodu. ryzyko tooreduce, można wybrać Biblioteka instrumentacji, takie jak [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), który jest częścią pakietu Microsoft ASP.NET Core. Ma platformy ASP.NET Core [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfejs, który można używać z dostawcy hello wybranych przez użytkownika, przy jednoczesnym zmniejszeniu hello wpływu na istniejący kod. Użyj kodu hello w ASP.NET Core w systemach Windows i Linux i w hello pełne .NET Framework, więc jest standardowym kodu instrumentacji. Jest to dodatkowe przedstawione poniżej:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Przy użyciu Microsoft.Extensions.Logging w sieci szkieletowej usług

1. Dodaj projekt toohello pakietu Microsoft.Extensions.Logging NuGet ma tooinstrument hello. Ponadto Dodaj wszelkie pakiety dostawcy (pakietu innych firm, zobacz poniższy przykład hello). Aby uzyskać więcej informacji, zobacz [logowanie do platformy ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).
2. Dodaj **przy użyciu** dyrektywy Microsoft.Extensions.Logging tooyour usługi pliku.
3. Zdefiniuj zmienną prywatny w klasie usługi.

  ```csharp
  private ILogger _logger = null;

  ```
4. W Konstruktorze hello klasie usługi Dodaj ten kod:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Uruchom kod w metody instrumentacji. Oto kilka przykładów:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Przy użyciu innych dostawców logowania

Niektóre dostawców Użyj podejście hello opisane w powyższej sekcji hello tym [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), i [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Możesz podłączyć każdego z nich do platformy ASP.NET Core rejestrowania lub można ich używać oddzielnie. Serilog jest funkcją, która wzbogaca wszystkich wiadomości wysłanych z rejestrator. Ta funkcja może być przydatna toooutput hello usługi nazwę, typ i informacji o partycji. toouse tę możliwość hello infrastruktury platformy ASP.NET Core, wykonaj następujące kroki:

1. Dodaj hello Serilog, Serilog.Extensions.Logging, i Serilog.Sinks.Observable dzaj pakietami nuget toohello projektu. Na przykład dalej hello należy również dodać Serilog.Sinks.Literate. Lepszym rozwiązaniem jest wyświetlany w dalszej części tego artykułu.
2. W Serilog należy utworzyć wystąpienia rejestratora LoggerConfiguration i hello.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Dodaj Konstruktor Serilog.ILogger argument toohello usługi i podaj hello nowo utworzony rejestratora.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. W Konstruktorze usługi hello, Dodaj hello następującego kodu, który tworzy hello enrichers właściwości dla hello **ServiceTypeName**, **ServiceName**, **PartitionId**i  **Identyfikator wystąpienia** właściwości hello usługi. Dodaje również właściwość enricher toohello fabryki rejestrowanie platformy ASP.NET Core, dzięki czemu można używać Microsoft.Extensions.Logging.ILogger w kodzie.

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. Kod hello dokumentu hello takie same jak przy użyciu platformy ASP.NET Core bez Serilog.

  >[!NOTE]
  >Firma Microsoft zaleca, że nie używasz hello static Log.Logger z hello poprzedzających przykład. Sieć szkieletowa usług może obsługiwać wiele wystąpień hello same usługi typu w ramach jednego procesu. Jeśli używasz hello Log.Logger statycznych, hello ostatniego składnika zapisywania programu enrichers właściwości hello wyświetli wartości dla wszystkich wystąpień, które są uruchomione. Jest jednym z powodów dlaczego hello _logger zmienna jest zmienną prywatnego elementu członkowskiego klasy usługi hello. Ponadto należy hello _logger dostępne toocommon kod, który może być używane w usługach.

## <a name="choosing-a-logging-provider"></a>Wybieranie dostawcy logowania

Jeśli aplikacja korzysta z wysokiej wydajności, **EventSource** zazwyczaj jest to dobre rozwiązanie. **Element EventSource** *zazwyczaj* wykorzystuje mniej zasobów i lepszą wydajność niż platformy ASP.NET Core rejestrowania lub dowolnym hello dostępnych rozwiązań innych firm.  To nie jest problemem w przypadku wielu usług, ale jeśli usługa jest ukierunkowane, za pomocą **EventSource** może być lepszym rozwiązaniem. Jednak tooget tych zalet strukturę rejestrowanie **EventSource** wymaga większych inwestycji zespołu inżynieryjnego. Jeśli to możliwe, czy szybkie prototyp kilka opcji rejestrowania, a następnie wybierz hello jedną, która najlepiej odpowiada Twoim potrzebom.

## <a name="next-steps"></a>Następne kroki

Po wybraniu użytkownika tooinstrument dostawcy rejestrowania aplikacji i usług z dzienników i zdarzeń muszą toobe zagregowane, zanim będzie można wysłać tooany analizy platformy. Przeczytaj informacje o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) i [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter zrozumieniu hello zalecane opcje.
