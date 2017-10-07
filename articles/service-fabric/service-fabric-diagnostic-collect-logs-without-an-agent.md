---
title: "Dzienniki aaaCollect bezpośrednio z usługi Azure Service Fabric procesu usługi | Microsoft Azure"
description: "W tym artykule opisano aplikacje będą mogły wysyłać dzienniki bezpośrednio tooa centralnej lokalizacji, takich jak Azure Application Insights lub Elasticsearch, bez polegania na agencie diagnostyki Azure sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Zbieranie dzienników bezpośrednio z procesu usługi sieć szkieletowa usług Azure
## <a name="in-process-log-collection"></a>W trakcie zbierania dzienników
Zbieranie aplikacji dzienników przy użyciu [rozszerzenia diagnostyki Azure](service-fabric-diagnostics-how-to-setup-wad.md) jest dobra opcja w przypadku **sieć szkieletowa usług Azure** usług Jeśli zbiór hello dziennika źródeł i miejsc docelowych jest mały, nie zmieni często, a jest prosta mapowania między hello źródeł i ich miejsc docelowych. Jeśli nie jest to alternatywa usług toohave ich wysłania dzienników przez użytkownika bezpośrednio tooa centralnej lokalizacji. Ten proces jest nazywany **zbierania dzienników w trakcie** i ma wiele potencjalnych korzyści:

* *Łatwe konfigurowanie i wdrażanie*

    * Konfiguracja Hello zbierania danych diagnostycznych jest tylko część hello konfiguracji usługi. Należy zachować łatwe tooalways go "zsynchronizowane" z hello pozostałej części aplikacji hello.
    * Dla każdej aplikacji lub na usługi konfiguracji jest łatwo osiągalny.
        * Zbieranie danych dziennika agenta na podstawie zwykle wymaga oddzielnego wdrażania i konfiguracji agenta diagnostyki hello, zadanie bardzo administracyjne i potencjalne źródła błędów. Często istnieje tylko jedno wystąpienie agenta hello dozwolonych dla jednej maszyny wirtualnej (węzeł) i konfiguracja agenta hello jest współdzielona przez wszystkie aplikacje i usługi uruchomione w tym węźle. 

* *Elastyczność*
   
    * Aplikacja Hello może wysyłać dane hello wszędzie tam, gdzie musi toogo, tak długo, jak istnieje biblioteki klienckiej, która obsługuje system przechowywania danych hello docelowe. Można dodać nowych miejsc docelowych pożądane.
    * Złożone zasady przechwytywania, filtrowania i agregacja danych może być zaimplementowany.
    * Zbieranie danych dziennika agenta na podstawie często jest ograniczona przez hello sink danych, które hello obsługuje agenta. Niektóre agenci są rozszerzalne.

* *Uzyskiwanie dostępu do danych aplikacji toointernal i kontekstu*
   
    * Podsystem diagnostycznych Hello uruchomiony proces aplikacji/usługi hello można łatwo rozszerzyć hello śladów z informacje kontekstowe.
    * Z kolekcją dziennika agenta na podstawie danych hello należy wysłać tooan agenta za pomocą mechanizmu komunikacji międzyprocesowej takich jak zdarzenia śledzenia systemu Windows. Ten mechanizm można skonfigurować dodatkowe ograniczenia.

Jest możliwe toocombine i korzystać z obu metod kolekcji. W rzeczywistości może być hello najlepsze rozwiązanie dla wielu aplikacji. Na podstawie agenta kolekcji to rozwiązanie fizyczne do zbierania dzienników toohello powiązane całego klastra, a poszczególne węzły klastra. To znacznie bardziej niezawodny sposób, niż zbierania dzienników w procesie, problemy z uruchamianiem usługi toodiagnose i awarii. Ponadto z wielu usług uruchomionych w klastrze usługi sieć szkieletowa, każda usługa swoją własną kolekcję dziennika w trakcie wykonywania powoduje wiele połączeń wychodzących z hello klastra. Duża liczba połączeń wychodzących jest opodatkowania zarówno w przypadku hello podsystemu sieci, jak i miejsce docelowe dziennika hello. Agent, takich jak [ **diagnostyki Azure** ](../cloud-services/cloud-services-dotnet-diagnostics.md) można zebrać dane z wielu usług i Wyślij wszystkie dane za pośrednictwem połączenia kilku, poprawy przepływności. 

W tym artykule zostanie przedstawiony sposób tooset w proces logowania przy użyciu kolekcji [ **biblioteki open source EventFlow**](https://github.com/Azure/diagnostics-eventflow). Inne biblioteki mogą być używane dla hello sam cel, ale EventFlow ma zaletą hello o został zaprojektowany specjalnie z myślą w trakcie dziennika kolekcji i toosupport usługi sieć szkieletowa usług. Używamy [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) jako miejsce docelowe dziennika hello. Innych miejsc docelowych, takich jak [ **usługi Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) lub [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) również są obsługiwane. Jest po prostu pytanie zainstalowania odpowiedniego pakietu NuGet i skonfigurowania hello docelowy w pliku konfiguracyjnym EventFlow hello. Aby uzyskać więcej informacji dotyczących miejsc docelowych dziennika innego niż usługi Application Insights, zobacz [dokumentacji EventFlow](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Dodawanie projektu usługi Service Fabric tooa EventFlow biblioteki
Pliki binarne EventFlow są dostępne jako zestaw pakietów NuGet. tooadd EventFlow tooa projektu usługi Service Fabric, kliknij prawym przyciskiem myszy projekt hello w hello Eksploratorze rozwiązań i wybierz polecenie "Manage NuGet packages". Przełącz kartę "Przeglądaj" toohello i wyszukaj "`Diagnostics.EventFlow`":

![Pakiety EventFlow NuGet w interfejs użytkownika Menedżera pakietów NuGet usługi Visual Studio][1]

Usługa Hello hosting EventFlow powinna zawierać odpowiednie pakiety w zależności od hello źródłowego i docelowego dla dzienników aplikacji hello. Dodaj hello następujące pakiety: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture danych z klasy EventSource hello usługi i EventSources standardowe, takie jak *usługi ServiceFabric* i *Microsoft-ServiceFabric-podmiotów*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (zamierzamy toosend hello dzienniki tooan Azure Application Insights zasobów)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (umożliwia inicjowanie potoku EventFlow hello z konfiguracji usługi Service Fabric i raporty problemów z wysyłaniem danych diagnostycznych jako raportów o kondycji sieci szkieletowej usług)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`pakiet wymaga tootarget projektu usługi hello .NET Framework 4.6 lub nowszą. Upewnij się, że platforma docelowa odpowiednie hello jest ustawiona we właściwościach projektu przed instalacją tego pakietu. 

Po wszystkich hello pakiety są zainstalowane, następnym krokiem hello jest tooconfigure i Włącz EventFlow w usłudze hello.

## <a name="configuring-and-enabling-log-collection"></a>Konfigurowanie i włączanie zbierania dzienników
Potok EventFlow odpowiedzialny za wysyłanie dzienników hello jest tworzona na podstawie specyfikacji przechowywane w pliku konfiguracji. `Microsoft.Diagnostics.EventFlow.ServiceFabric`Pakiet instaluje plik początkowej konfiguracji EventFlow pod `PackageRoot\Config` folder rozwiązania. Nazwa pliku Hello jest `eventFlowConfig.json`. Ten plik konfiguracyjny musi toobe zmodyfikować toocapture danych z usługi domyślne hello `EventSource` klasy i wysyłania usługi Insights tooApplication danych.

> [!NOTE]
> Przyjęto założenie, że czytelnik zna **Azure Application Insights** service i czy masz zasobu usługi Application Insights planowanie toouse toomonitor usługi sieć szkieletowa usług. Aby uzyskać więcej informacji, zobacz [utworzyć zasobu usługi Application Insights](../application-insights/app-insights-create-new-resource.md).

Otwórz hello `eventFlowConfig.json` w edytorze hello i zmieniać jego zawartości, jak pokazano poniżej. Upewnij się, że nazwa ServiceEventSource hello tooreplace i zgodnie z toocomments klucza Instrumentacji usługi Application Insights. 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> Nazwa Hello ServiceEventSource usługi jest hello wartość właściwości Name elementu hello hello `EventSourceAttribute` stosowane toohello ServiceEventSource klasy. Wszystkie określono w hello `ServiceEventSource.cs` pliku, który jest częścią hello kodu usługi. Na przykład na powitania następujący kod fragment hello nazwa hello ServiceEventSource to *Moja firma-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Należy pamiętać, że `eventFlowConfig.json` plik jest częścią pakietu konfiguracji usługi. Plik toothis zmiany mogą być zawarte w pełnej lub Konfiguracja — tylko do uaktualnienia usługi hello, tooService temat sieci szkieletowej uaktualnienia kontroli kondycji i automatycznego wycofania w przypadku niepowodzenia uaktualnienia. Aby uzyskać więcej informacji, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).

Ostatnim krokiem Hello jest tooinstantiate EventFlow potoku w kodzie uruchamiania usługi, znajduje się w `Program.cs` pliku. Hello następującymi dodatkami związanych z EventFlow przykład są oznaczane komentarze, począwszy od `****`:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

Nazwa Hello przekazywana jako parametr hello hello `CreatePipeline` metody hello `ServiceFabricDiagnosticsPipelineFactory` jest nazwą hello hello *jednostki kondycji* reprezentujący hello EventFlow dziennika kolekcji potoku. Ta nazwa jest używana, jeśli EventFlow napotkał błąd i zgłasza za pośrednictwem hello podsystemu kondycji sieci szkieletowej usług.

## <a name="verification"></a>Weryfikacja
Uruchomić usługę i sprawdź hello debugowania okno dane wyjściowe w programie Visual Studio. Po uruchomieniu usługi hello powinny zacząć się wyświetlać dowód, że usługa wysyła rekordy "Telemetrię usługi Application Insights". Otwórz przeglądarkę sieci web i przejdź tooyour przejście zasobu usługi Application Insights. Otwórz kartę "Wyszukaj" (u góry hello hello domyślne "Overview" bloku). Z niewielkim opóźnieniem powinny zacząć się wyświetlać dane śledzenia w portalu usługi Application Insights hello:

![Portal usługi Application Insights wyświetlanie dzienników aplikacji sieci szkieletowej usług][2]

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat diagnozowania i monitorowanie usługi sieci szkieletowej usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Dokumentacja EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
