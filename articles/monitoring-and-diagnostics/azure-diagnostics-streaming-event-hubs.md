---
title: "aaaStreaming danych diagnostycznych platformy Azure w ścieżce aktywnej hello za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Konfigurowania diagnostyki Azure z usługą Event Hubs końcowy tooend, w tym wskazówki dotyczące typowych scenariuszy."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Strumieniowe przesyłanie danych diagnostycznych platformy Azure w ścieżce aktywnej hello za pomocą usługi Event Hubs
Diagnostyka Azure oferuje elastyczne metody toocollect metryki i loguje się z usługi w maszynach wirtualnych (VM) w chmurze i przenieść tooAzure wyniki magazynu. Począwszy od przedział czasu hello marca 2016 (zestaw SDK 2.9) można wysyłać toocustom diagnostyki źródeł danych i transferu danych ścieżkę aktywną w ciągu sekund za pomocą [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

Obsługiwane typy danych obejmują:

* Zdarzenia funkcji Śledzenie zdarzeń systemu Windows (ETW)
* Liczniki wydajności
* Dzienniki zdarzeń systemu Windows
* Dzienniki aplikacji
* Dzienników infrastruktury Diagnostyka Azure

W tym artykule opisano, jak tooconfigure diagnostyki Azure z usługą Event Hubs od zakończenia tooend. Także wskazówki dotyczące hello następujące typowe scenariusze:

* Sposób rejestrowania toocustomize hello i metryki, które jest wysyłana tooEvent koncentratory
* Sposób konfiguracji toochange w każdym środowisku.
* Jak usługa Event Hubs tooview strumienia danych
* Jak tootroubleshoot hello połączenia  

## <a name="prerequisites"></a>Wymagania wstępne
Dane receieving centra zdarzeń z diagnostyki Azure jest obsługiwana w usługi w chmurze, maszyn wirtualnych, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług w programie hello Azure SDK 2.9 i hello odpowiadającego Azure Tools dla programu Visual Studio.

* Rozszerzenie diagnostyki Azure 1.6 ([zestawu Azure SDK dla programu .NET 2.9 lub nowszego](https://azure.microsoft.com/downloads/) dotyczy to domyślnie)
* [Visual Studio 2013 lub nowszy](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Istniejące konfiguracje diagnostyki Azure w aplikacji przy użyciu *.wadcfgx* pliku i jedną z następujących metod hello:
  * Visual Studio: [Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyny wirtualne](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Program Windows PowerShell: [Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Przestrzeń nazw centra zdarzeń udostępniane na artykuł hello [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Połącz zbiornika koncentratory tooEvent diagnostyki Azure
Domyślnie diagnostyki Azure zawsze wysyła dzienniki i metryki tooan konta magazynu Azure. Aplikacja może również wysłać tooEvent danych koncentratory, dodając nową **wychwytywanie** w sekcji hello **PublicConfig** / **WadCfg** element hello *.wadcfgx* pliku. W programie Visual Studio hello *.wadcfgx* plik jest przechowywany w hello następującej ścieżki: **projekt usługi w chmurze** > **ról** > **() RoleName)** > **diagnostics.wadcfgx** pliku.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

W tym przykładzie hello Centrum zdarzeń jest ustawiony adres URL toohello pełni kwalifikowanych nazw Centrum zdarzeń hello: przestrzeń nazw usługi Event Hubs + "/" + Nazwa Centrum zdarzeń.  

adres URL jest wyświetlany w hello Centrum zdarzeń Hello [portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) na pulpicie nawigacyjnym usługi Event Hubs hello.  

Witaj **Sink** nazwa może być ustawiona prawidłowy ciąg tooany tak długo, jak hello tę samą wartość jest używana przez całą hello pliku konfiguracji.

> [!NOTE]
> Mogą istnieć dodatkowe wychwytywanie, takich jak *applicationInsights* skonfigurowane w tej sekcji. Diagnostyka Azure umożliwia jeden lub więcej wychwytywanie toobe zdefiniowana, jeśli każdy obiekt sink jest również zadeklarowany w hello **PrivateConfig** sekcji.  
>
>

Hello zbiornika centra zdarzeń należy również zadeklarowana i zdefiniowanych w hello **PrivateConfig** sekcji hello *.wadcfgx* pliku konfiguracji.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Witaj `SharedAccessKeyName` wartości muszą być zgodne, klucz dostępu sygnatury dostępu Współdzielonego i zasad, który został zdefiniowany w hello **centra zdarzeń** przestrzeni nazw. Przeglądaj pulpitu nawigacyjnego usługi Event Hubs toohello w hello [portalu Azure](https://manage.windowsazure.com), kliknij przycisk hello **Konfiguruj** , a następnie skonfigurować zasadę nazwanych (na przykład "SendRule"), która ma *wysyłania* uprawnienia. Witaj **StorageAccount** jest również zadeklarowany w **PrivateConfig**. Nie jest konieczne tutaj wartości toochange jeśli działają. W tym przykładzie firma Microsoft może pozostać hello wartości puste, co jest znak czy podrzędne zasobów spowoduje ustawienie wartości hello. Na przykład Witaj *ServiceConfiguration.Cloud.cscfg* pliku konfiguracji środowiska ustawia hello odpowiednie środowisko nazwy i kluczy.  

> [!WARNING]
> klucz sygnatury dostępu Współdzielonego centra zdarzeń Hello jest przechowywany w postaci zwykłego tekstu w hello *.wadcfgx* pliku. Często ten klucz jest zaewidencjonowany toosource kontroli kodu lub jest dostępna jako zasób w serwerze kompilacji, więc należy je chronić, zależnie od potrzeb. Zalecane jest użycie klucza sygnatury dostępu Współdzielonego tutaj z *wysłać tylko* uprawnienia tak, aby złośliwy użytkownik można zapisać toohello Centrum zdarzeń, ale nie nasłuchiwania tooit lub zarządzać nim.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Skonfiguruj diagnostyki Azure toosend dzienniki i metryki tooEvent koncentratory
Zgodnie z opisem wcześniej, wszystkie domyślne i dane diagnostyki niestandardowej, oznacza to, metryki i dzienniki, są wysyłane automatycznie tooAzure magazynu z interwałem hello skonfigurowane. Centra zdarzeń i wszelkie dodatkowe zbiornika w toobe hierarchii hello wysyłane toohello Centrum zdarzeń można określić dowolnego węzła głównego lub typu liść. W tym zdarzenia ETW, liczniki wydajności, dzienniki zdarzeń systemu Windows i dzienników aplikacji.   

Koniecznie tooconsider liczbę punktów danych faktycznie powinna być przetransferowane tooEvent koncentratorów. Zwykle deweloperzy transferu danych hot ścieżki małe opóźnienia, który musi być używane i szybko interpretowane. Przykłady są systemy monitorowania, alertów lub reguły automatycznego skalowania. Deweloper może również skonfigurować Magazyn alternatywnego analizy lub Wyszukaj magazynu — na przykład usługi Azure Stream Analytics, Elasticsearch, system monitorowania niestandardowe lub Ulubione system monitorowania od innych użytkowników.

Witaj poniżej przedstawiono niektóre przykładowe konfiguracje.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

W hello powyżej przykładzie, zbiornika hello jest nadrzędny zastosowane toohello **liczniki wydajności** węzeł w hierarchii hello, co oznacza, że wszystkie podrzędne **liczniki wydajności** będą wysyłane tooEvent koncentratorów.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

W poprzednim przykładzie hello zbiornika hello jest zastosowane tooonly trzy liczniki: **żądania w kolejce**, **odrzucenia żądania**, i **% czasu procesora**.  

Witaj poniższy przykład przedstawia sposób deweloper może ograniczyć hello ilość danych wysłanych toobe hello krytyczne metryki, które są używane dla tej usługi kondycji.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

W tym przykładzie zbiornika hello jest stosowane toologs i filtrowane tylko tooerror śledzenia poziomu.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Wdrażanie i aktualizacji aplikacji i informacji diagnostycznych konfiguracji usługi w chmurze
Visual Studio udostępnia hello najprostszym ścieżki toodeploy hello aplikacji i konfigurowanie zbiornika usługi Event Hubs. Plik hello tooview i edytowanie, otwórz hello *.wadcfgx* plików w programie Visual Studio, go edytować i zapisać go. Ścieżka Hello jest **projekt usługi w chmurze** > **ról** > **(RoleName)** > **diagnostics.wadcfgx**.  

W tym momencie wszystkie wdrożenia i wdrożenia aktualizacji w Visual Studio, Visual Studio Team System i wszystkie polecenia lub skryptów, które są oparte na MSBuild i użyj hello akcje **/t: publikowanie** docelowy obejmują hello *.wadcfgx*  w procesie tworzenia pakietów hello. Ponadto wdrożenia i aktualizacje wdrożyć hello tooAzure pliku przy użyciu hello odpowiednie rozszerzenie agenta diagnostyki Azure na maszyny wirtualne.

Po wdrożeniu aplikacji hello i konfiguracji diagnostyki Azure, będzie wyświetlany natychmiast działania na pulpicie nawigacyjnym hello hello Centrum zdarzeń. Oznacza to, że wszystko jest gotowe toomove na tooviewing hello hot ścieżki danych hello odbiornika klienta lub analizy dowolnego narzędzia.  

W następującej ilustracji hello pulpit nawigacyjny usługi Event Hubs hello pokazuje, dobrej kondycji wysyłania diagnostyki danych toohello zdarzenia koncentratora początkowych pewnego czasu po 23: 00. Kiedy jest hello aplikacja została wdrożona z zaktualizowaną *.wadcfgx* plików i hello zbiornika zostało skonfigurowane prawidłowo.

![][0]  

> [!NOTE]
> Po wprowadzeniu pliku konfiguracji diagnostyki Azure toohello aktualizacji (.wadcfgx), zaleca się push hello aktualizacje toohello całej aplikacji, a także hello konfiguracji za pomocą programu Visual Studio publikowania lub skrypt programu Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Dane widoku dynamicznego ścieżki
Jak wcześniej wspomniano, istnieje wiele przypadki użycia nasłuchiwania tooand przetwarzania danych usługi Event Hubs.

Jednym z podejść proste jest toocreate z Centrum testów małych konsoli aplikacji toolisten toohello zdarzeń i drukowania hello strumienia wyjściowego. Możesz umieścić hello następującego kodu, który jest co omówiono bardziej szczegółowo w [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), w aplikacji konsoli.  

Należy pamiętać, że aplikacja konsolowa hello musi zawierać hello [pakietu NuGet hosta procesora zdarzeń](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Pamiętaj tooreplace hello wartości w nawiasy w hello **Main** funkcji z wartościami dla zasobów.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Rozwiązywanie problemów z wychwytywanie centra zdarzeń
* Centrum zdarzeń Hello nie są wyświetlane zdarzenia przychodzącego lub wychodzącego działania zgodnie z oczekiwaniami.

    Sprawdź, czy Centrum zdarzeń jest pomyślnie zainicjowano obsługę administracyjną. Wszystkie informacje o połączeniu w hello **PrivateConfig** sekcji *.wadcfgx* musi odpowiadać wartości hello zasobu w portalu hello. Upewnij się, że masz SAS zasady zdefiniowane ("SendRule" w przykładzie hello) w portalu hello, który *wysyłania* uprawnienia.  
* Po zaktualizowaniu Centrum zdarzeń hello nie jest już wyświetlana działania zdarzenia przychodzącego lub wychodzącego.

    Najpierw upewnij się, że hello Centrum zdarzeń i informacje o konfiguracji są poprawne, jak opisano wcześniej. Czasami hello **PrivateConfig** jest resetowany w aktualizacji wdrożenia. Witaj zalecane jest poprawka toomake wszystkie zmiany zbyt*.wadcfgx* w hello projektu, a następnie Wypchnij aktualizacji kompletna aplikacja. Jeśli nie jest to możliwe, upewnij się, aktualizacja diagnostyki hello wypchnięcia pełnego **PrivateConfig** zawierającą hello klucza sygnatury dostępu Współdzielonego.  
* Próbuję hello sugestie i Centrum zdarzeń hello nadal nie działa.

    Należy przejrzeć hello Azure Storage tabeli, która zawiera dzienniki i błędy diagnostyki Azure, sama: **WADDiagnosticInfrastructureLogsTable**. Jedną z opcji jest toouse narzędzia, takie jak [Eksploratora usługi Storage Azure](http://www.storageexplorer.com) tooconnect toothis konta magazynu, wyświetlić tę tabelę i Dodaj zapytanie dla sygnatury czasowej w hello ostatnich 24 godzinach. Można użyć hello narzędzia tooexport plik CSV i otwórz go w aplikacji, takich jak program Microsoft Excel. Excel umożliwia łatwe toosearch ciągi karty telefonicznej, takich jak **EventHubs**, jakie błąd jest zgłaszany toosee.  

## <a name="next-steps"></a>Następne kroki
• [Dowiedz się więcej o usłudze Event Hubs](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Dodatek: Ukończyć przykład pliku (.wadcfgx) konfiguracji diagnostyki Azure
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

uzupełniające Hello *ServiceConfiguration.Cloud.cscfg* dla tego przykładu wygląda hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Odpowiednik Json na podstawie ustawień maszyny wirtualnej jest następujący:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](../event-hubs/event-hubs-create.md)
* [Event Hubs — często zadawane pytania](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
