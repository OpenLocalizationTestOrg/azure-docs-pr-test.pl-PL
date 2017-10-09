---
title: "Usługi sieci szkieletowej zdarzeń agregacji z EventFlow aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat agregowania i zbierania zdarzeń przy użyciu EventFlow monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
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
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Agregacja zdarzeń i kolekcji przy użyciu EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) może kierować zdarzenia z tooone węzła lub więcej monitorowania miejsc docelowych. Ponieważ jest uwzględniona jako pakietu NuGet w projekcie usługi, EventFlow kod i konfiguracja są przesyłane z usługą hello, eliminując problem z konfiguracją każdego węzła hello wymienione wcześniej o diagnostyki Azure. EventFlow jest uruchamiany w ramach procesu usługi i łączy się bezpośrednio toohello skonfigurowany w danych wyjściowych. Ze względu na powitania bezpośrednie połączenie EventFlow działa platformy Azure, kontenera i lokalnego wdrożenia usługi. Należy zachować ostrożność, jeśli uruchomisz EventFlow w scenariuszach wysokiej gęstości, takich jak w kontenerze, ponieważ każdy potoku EventFlow sprawia, że połączenie zewnętrzne. Tak Jeśli host kilka procesów, możesz uzyskać kilka połączeń wychodzących! Nie jest to tyle problemem w przypadku aplikacji usługi Service Fabric, ponieważ wszystkie repliki `ServiceType` Uruchom w hello tego samego procesu, i ogranicza hello liczby połączeń wychodzących. EventFlow oferuje również filtrowanie zdarzeń, tak aby były wysyłane tylko zdarzenia hello zgodne hello określony filtr.

## <a name="setting-up-eventflow"></a>Konfigurowanie EventFlow

Pliki binarne EventFlow są dostępne jako zestaw pakietów NuGet. tooadd EventFlow tooa projektu usługi Service Fabric, kliknij prawym przyciskiem myszy projekt hello w hello Eksploratorze rozwiązań i wybierz polecenie "Manage NuGet packages". Przełącz kartę "Przeglądaj" toohello i wyszukaj "`Diagnostics.EventFlow`":

![Pakiety EventFlow NuGet w interfejs użytkownika Menedżera pakietów NuGet usługi Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Zostanie wyświetlona lista pakietów różnych wyświetlani, etykietą "Danych wejściowych" i "Generuje". EventFlow obsługuje różne analizatory i rejestrowania różnych dostawców. Usługa Hello hosting EventFlow powinna zawierać odpowiednie pakiety w zależności od hello źródłowego i docelowego dla dzienników aplikacji hello. Ponadto toohello core ServiceFabric pakietu, należy również co najmniej jeden przychodzących i wychodzących, skonfigurować. W przypadku exmaple można dodać następujące pakiety toosent EventSource zdarzenia tooApplication Insights hello:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture danych z klasy EventSource hello usługi i EventSources standardowe, takie jak *usługi ServiceFabric* i *Microsoft-ServiceFabric-podmiotów*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(zamierzamy toosend hello dzienniki tooan Azure Application Insights zasobów)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(umożliwia inicjowanie potoku EventFlow hello z konfiguracji usługi Service Fabric i raporty problemów z wysyłaniem danych diagnostycznych jako raportów o kondycji sieci szkieletowej usług)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`pakiet wymaga tootarget projektu usługi hello .NET Framework 4.6 lub nowszą. Upewnij się, że platforma docelowa odpowiednie hello jest ustawiona we właściwościach projektu przed instalacją tego pakietu.

Po wszystkich hello pakiety są zainstalowane, następnym krokiem hello jest tooconfigure i Włącz EventFlow w usłudze hello.

## <a name="configuring-and-enabling-log-collection"></a>Konfigurowanie i włączanie zbierania dzienników
potok EventFlow Hello jest odpowiedzialny za wysyłanie dzienników hello jest tworzona na podstawie specyfikacji przechowywane w pliku konfiguracji. Witaj `Microsoft.Diagnostics.EventFlow.ServiceFabric` pakiet instaluje plik początkowej konfiguracji EventFlow pod `PackageRoot\Config` folder rozwiązania o nazwie `eventFlowConfig.json`. Ten plik konfiguracyjny musi toobe zmodyfikować toocapture danych z usługi domyślne hello `EventSource` klasy i wszystkie inne dane wejściowe tooconfigure, a następnie Wyślij dane toohello odpowiednie miejsce.

Poniżej przedstawiono przykładowe *eventFlowConfig.json* oparte na powitania pakietów NuGet wymienionych powyżej:
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

Nazwa Hello ServiceEventSource usługi jest hello wartość właściwości Name elementu hello hello `EventSourceAttribute` stosowane toohello ServiceEventSource klasy. Wszystkie określono w hello `ServiceEventSource.cs` pliku, który jest częścią hello kodu usługi. Na przykład na powitania następujący kod fragment hello nazwa hello ServiceEventSource to *Moja firma-Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Należy pamiętać, że `eventFlowConfig.json` plik jest częścią pakietu konfiguracji usługi. Plik toothis zmiany mogą być zawarte w pełnej lub Konfiguracja — tylko do uaktualnienia usługi hello, tooService temat sieci szkieletowej uaktualnienia kontroli kondycji i automatycznego wycofania w przypadku niepowodzenia uaktualnienia. Aby uzyskać więcej informacji, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).

Witaj *filtry* sekcji konfiguracji hello umożliwia toofurther dostosować informacje hello toogo będzie hello EventFlow potoku toohello danych wyjściowych w, dzięki czemu toodrop uwzględnienia niektórych informacji lub zmienić hello Struktura hello danych zdarzenia. Aby uzyskać więcej informacji dotyczących filtrowania, zobacz [filtry EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

Ostatnim krokiem Hello jest tooinstantiate EventFlow potoku w kodzie uruchamiania usługi, znajduje się w `Program.cs` pliku:

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

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Przy użyciu ustawień sieci szkieletowej usług oraz eventFlowConfig tooin parametry aplikacji

Obsługuje EventFlow przy użyciu ustawień sieci szkieletowej usług oraz ustawienia EventFlow tooconfigure parametry aplikacji. Może się odwoływać parametrów ustawień sieci szkieletowej tooService przy użyciu tej składni specjalne wartości:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`to nazwa hello hello sekcji konfiguracji sieci szkieletowej usług, i `<setting-name>` jest ustawienie konfiguracji hello podawania wartości hello, które będzie używane tooconfigure ustawienie EventFlow. więcej informacji na temat tooread toodo, przejdź zbyt[obsługę ustawień sieci szkieletowej usług i aplikacji parametry](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Weryfikacja

Uruchomić usługę i sprawdź hello debugowania okno dane wyjściowe w programie Visual Studio. Po uruchomieniu usługi hello powinny zacząć się wyświetlać się, że dowód, który wysyła usługi rejestruje dane wyjściowe toohello, który został skonfigurowany. Przejdź tooyour zdarzenie analizy i wizualizacji platformy i upewnij się, że dzienniki rozpoczęły tooshow up (może to potrwać kilka minut).

## <a name="next-steps"></a>Następne kroki

* [Analiza zdarzeń i wizualizacji z usługą Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analiza zdarzeń i wizualizacji z OMS](service-fabric-diagnostics-event-analysis-oms.md)
* [Dokumentacja EventFlow](https://github.com/Azure/diagnostics-eventflow)