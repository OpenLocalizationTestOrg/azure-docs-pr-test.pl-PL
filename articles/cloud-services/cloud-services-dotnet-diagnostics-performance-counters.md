---
title: "Liczniki wydajności w diagnostyce Azure aaaUse | Dokumentacja firmy Microsoft"
description: "Użyj liczników wydajności usługi w chmurze platformy Azure lub wąskich gardeł toofind maszyny wirtualnej i dostrajania wydajności."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Tworzenie i używanie liczników wydajności w aplikacji Azure
W tym artykule opisano hello zalet i jak liczniki wydajności tooput do aplikacji platformy Azure. Można ich używać danych toocollect, Znajdź wąskich gardeł i dostrajania wydajności systemu i aplikacji.

Liczniki wydajności są dostępne dla systemu Windows Server, IIS i platformy ASP.NET można także gromadzić i używane kondycji hello toodetermine role sieci web platformy Azure, roli proces roboczy i maszyn wirtualnych. Można również utworzyć i używać niestandardowe liczniki wydajności.  

Należy zbadać dane licznika wydajności

1. Bezpośrednio na hoście aplikacji hello za pomocą narzędzia Monitor wydajności hello dostęp za pomocą pulpitu zdalnego
2. Przy użyciu programu System Center Operations Manager hello Azure pakietu administracyjnego
3. Przy użyciu innych narzędzi monitorowania, które uzyskują dostęp do hello danych diagnostycznych transferu tooAzure magazynu. Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) Aby uzyskać więcej informacji.  

Aby uzyskać więcej informacji na temat monitorowania wydajności aplikacji hello hello [portalu Azure](http://portal.azure.com/), zobacz [jak usług w chmurze tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Aby uzyskać dodatkowe szczegółowe wskazówki na temat tworzenia rejestrowania i śledzenia strategii i przy użyciu innych technik tootroubleshoot problemów i Diagnostyka i optymalizowanie aplikacji Azure, zobacz [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia Azure Aplikacje](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Aby włączyć monitorowanie licznika wydajności
Liczniki wydajności nie są domyślnie włączone. Aplikacja lub zadanie uruchamiania należy zmodyfikować diagnostyki domyślne hello liczników wydajności zależnych hello tooinclude konfiguracji agenta, że chcesz toomonitor dla każdego wystąpienia roli.

### <a name="performance-counters-available-for-microsoft-azure"></a>Liczniki wydajności dostępne platformy Microsoft Azure
Platforma Azure udostępnia podzbiór hello dostępnych liczników wydajności dla systemu Windows Server, IIS i hello stosu ASP.NET. Witaj poniższej tabeli wymieniono niektóre liczniki wydajności hello szczególne znaczenie dla aplikacji platformy Azure.

| Kategoria licznika: Obiektu (wystąpienia) | Nazwa licznika | Dokumentacja |
| --- | --- | --- |
| Wyjątki środowiska CLR platformy .NET (*globalne*) |# Clr\\liczba wyjątków / s |Liczniki wydajności wyjątku |
| .NET CLR pamięci (*globalne*) |% Czasu odzyskiwania pamięci |Liczniki wydajności pamięci |
| ASP.NET |Aplikacja zostanie uruchomiona ponownie |Liczniki wydajności dla programu ASP.NET |
| ASP.NET |Czas wykonania żądania |Liczniki wydajności dla programu ASP.NET |
| ASP.NET |Liczba żądań rozłączonych |Liczniki wydajności dla programu ASP.NET |
| ASP.NET |Ponowne uruchomienie procesu roboczego |Liczniki wydajności dla programu ASP.NET |
| Aplikacji programu ASP.NET (**całkowita**) |Całkowita liczba żądań |Liczniki wydajności dla programu ASP.NET |
| Aplikacji programu ASP.NET (**całkowita**) |Żądania na sekundę |Liczniki wydajności dla programu ASP.NET |
| ASP.NET 4.0.30319 |Czas wykonania żądania |Liczniki wydajności dla programu ASP.NET |
| ASP.NET 4.0.30319 |Czas oczekiwania na żądanie |Liczniki wydajności dla programu ASP.NET |
| ASP.NET 4.0.30319 |Bieżące żądania |Liczniki wydajności dla programu ASP.NET |
| ASP.NET 4.0.30319 |Liczba żądań w kolejce |Liczniki wydajności dla programu ASP.NET |
| ASP.NET 4.0.30319 |Liczba żądań odrzuconych |Liczniki wydajności dla programu ASP.NET |
| Memory (Pamięć) |Dostępna pamięć (MB) |Liczniki wydajności pamięci |
| Memory (Pamięć) |Zadeklarowane bajty |Liczniki wydajności pamięci |
| Procesor(_Total) |Czas procesora (%) |Liczniki wydajności dla programu ASP.NET |
| TCPv4 |Liczba błędów połączenia |Obiekt TCP |
| TCPv4 |Połączeń |Obiekt TCP |
| TCPv4 |Resetowanie połączenia |Obiekt TCP |
| TCPv4 |Segmenty wysłane/s |Obiekt TCP |
| Interface(*) sieci |Bajty odebrane/s |Obiekt interfejsu sieciowego |
| Interface(*) sieci |Bajty wysłane/s |Obiekt interfejsu sieciowego |
| Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci) |Bajty odebrane/s |Obiekt interfejsu sieciowego |
| Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci) |Bajty wysłane/s |Obiekt interfejsu sieciowego |
| Interfejs sieciowy (_2 karty magistrali maszyny wirtualnej Microsoft sieci) |Całkowita liczba bajtów/s |Obiekt interfejsu sieciowego |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Tworzenie i dodawanie aplikacji tooyour liczniki wydajności niestandardowych
Azure ma toocreate pomocy technicznej i zmodyfikuj niestandardowe liczniki wydajności dla ról sieci web i proces roboczy. Hello liczniki mogą być używane tootrack i monitorowanie zachowania specyficzne dla aplikacji. Można tworzyć i usuwanie kategorii licznika wydajności niestandardowych i specyfikatory zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.

> [!NOTE]
> Kod, który zmienia toocustom liczników wydajności mają podwyższony poziom uprawnień toorun. Jeśli kod hello jest w roli sieci web lub roli proces roboczy, hello roli musi zawierać znacznik hello <Runtime executionContext="elevated" /> w hello ServiceDefinition.csdef plików dla tooinitialize roli hello poprawnie.
>
>

Możesz wysłać wydajność — niestandardowy licznik tooAzure zapisywanie danych przy użyciu hello Diagnostyka agenta.

dane licznika wydajności standardowe Hello jest generowany przez hello Azure przetwarzania. Dane licznika wydajności niestandardowych muszą być utworzone przez aplikację sieci web roli lub procesu roboczego roli. Zobacz [typy licznika wydajności](https://msdn.microsoft.com/library/z573042h.aspx) informacje o typach hello danych, które mogą być przechowywane w niestandardowe liczniki wydajności. Zobacz [próbki liczniki wydajności](http://code.msdn.microsoft.com/azure/) na przykład, które tworzy i ustawia dane licznika wydajności niestandardowych w roli sieci web.

## <a name="store-and-view-performance-counter-data"></a>Magazyn i widoku danych licznika wydajności
Azure przechowuje dane licznika wydajności z innych informacji diagnostycznych. Te dane są dostępne dla monitorowania zdalnego wystąpienia roli hello jest uruchomiona za pomocą narzędzi tooview dostępu do pulpitu zdalnego, takich jak monitora wydajności. toopersist hello poza hello wystąpienia roli, agenta diagnostyki hello musi transferu danych hello tooAzure pamięci masowej. limit rozmiaru Hello danych licznika wydajności hello w pamięci podręcznej, można skonfigurować w hello Diagnostyka agenta lub może być skonfigurowane toobe częścią udostępnionego limit hello wszystkich danych diagnostycznych. Aby uzyskać więcej informacji na temat ustawiania rozmiaru buforu hello, zobacz [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) i [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Zobacz [magazynu i widoku danych diagnostycznych w usłudze Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) omówienie konfigurowania konta magazynu tooa danych tootransfer hello Diagnostyka agenta.

Każde wystąpienie licznika wydajności skonfigurowany jest rejestrowana w określonym próbkowania i hello pobrane dane są przesyłane toohello konta magazynu przez żądanie transferu zaplanowanego lub żądanie transferu na żądanie. Przeniesienia automatyczne może zostać zaplanowane tak często, jak jeden raz na minutę. Dane licznika wydajności przekazywane przez agenta diagnostyki hello są przechowywane w tabeli, WADPerformanceCountersTable, hello konta magazynu. Ta tabela może uzyskać dostępu do i wykonać zapytania z metody interfejsu API magazynu Azure w warstwie standardowa. Zobacz [przykład liczniki wydajności programu Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) przykład kwerend i wyświetlanie danych licznika wydajności z hello WADPerformanceCountersTable tabeli.

> [!NOTE]
> W zależności od hello Diagnostyka agenta transferu częstotliwość i czas oczekiwania w kolejce hello najnowsze dane liczników wydajności na koncie magazynu hello może potrwać kilka minut nieaktualny.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Włącz użycie pliku konfiguracji diagnostyki liczniki wydajności
Użyj hello następujące liczniki wydajności tooenable procedury w aplikacji platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne
W tej sekcji założono, że zaimportowane hello monitor diagnostyki aplikacji i dodać hello diagnostyki konfiguracji pliku tooyour rozwiązania Visual Studio (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym). Zobacz kroki 1 i 2 w [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md)) Aby uzyskać więcej informacji.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Krok 1: Zbieranie i przechowywanie danych z liczników wydajności
Po dodaniu diagnostyki hello plików rozwiązania Visual Studio tooyour hello zbieranie i przechowywanie danych licznika wydajności można skonfigurować w aplikacji Azure. Jest to realizowane przez dodanie pliku diagnostyki toohello liczników wydajności. W wystąpieniu hello najpierw zbieranych danych diagnostycznych, łącznie z liczników wydajności. Hello dane są następnie utrwalonego toohello WADPerformanceCountersTable tabeli w hello usługi tabel Azure, więc będzie również konieczne toospecify hello konta magazynu w aplikacji. Jeśli testujesz aplikację w lokalnie w hello obliczeniowe emulatora, można również przechowywać dane diagnostyczne lokalnie w hello emulatora magazynu. Przed zapisaniem danych diagnostycznych, należy najpierw przejść toohello [portalu Azure](http://portal.azure.com/) i Utwórz konto magazynu klasycznego. Najlepszym rozwiązaniem jest toolocate konta magazynu w hello tej samej lokalizacji geograficznej jako aplikacji platformy Azure. Przy zachowaniu hello Azure aplikacji i konto magazynu są w hello tej samej lokalizacji geograficznej, uniknąć kosztów przepustowości zewnętrznych płatności i zmniejszenia opóźnień.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Dodaj plik diagnostyki toohello liczników wydajności
Istnieje wiele liczników, których można użyć. Witaj poniższym przykładzie pokazano kilka liczniki wydajności, które są zalecane sieci web i monitorowania roli procesu roboczego.

Otwórz plik diagnostyki hello (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i Dodaj hello następującego elementu DiagnosticMonitorConfiguration toohello:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

Atrybut bufferQuotaInMB Hello, który określa hello maksymalną ilość pamięci systemu plików, która jest dostępna dla typu kolekcji danych hello (Azure dzienniki, dzienniki programu IIS, itp.). Witaj domyślna to 0. Zostanie osiągnięty przydział hello, hello najstarsze dane są usuwane po dodaniu nowych danych. Witaj sumę wszystkich właściwości bufferQuotaInMB hello musi być większa niż wartość hello hello OverallQuotaInMB atrybutu. Bardziej szczegółowe omówienie określania, ile miejsca do magazynowania jest wymagana w przypadku hello zbierania danych diagnostycznych, zobacz hello sekcji konfiguracji WAD [Rozwiązywanie problemów z najlepszych rozwiązań dotyczących tworzenia aplikacji Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

Witaj scheduledTransferPeriod atrybut, który określa interwał powitania między zaplanowane transferów danych, zaokrąglona w górę toohello najbliższej minutę. W hello następujące przykłady jest ustawiona tooPT30M (30 minut). Ustawienie hello transfer okresu tooa mała wartość, na przykład 1 minutę, obniży wydajności aplikacji w środowisku produkcyjnym, ale może być przydatne przy przeglądaniu diagnostyki Postaramy się szybko podczas testowania. okres zaplanowanego transferu Hello powinien być duże tooensure danych diagnostycznych nie jest zastąpione na powitania wystąpienia, ale wystarczająco duży, że nie ma wpływu hello wydajność aplikacji.

Atrybut counterSpecifier Hello określa toocollect licznika wydajności hello. Atrybut sampleRate Hello określa szybkość hello, w którym licznik wydajności hello powinny być pobrane, w tym przypadku 30 sekund.

Po dodaniu się, że liczniki wydajności hello, które mają toocollect zapisać zmiany toohello diagnostyki. Następnie należy konto magazynu hello toospecify zostaną utrwalone hello danych diagnostycznych.

### <a name="specify-hello-storage-account"></a>Określ konto magazynu hello
toopersist konta użytkownika tooyour informacji diagnostyki Azure Storage, należy określić parametry połączenia w pliku konfiguracyjnym (pliku ServiceConfiguration.cscfg) usługi.

Dla 2.5 zestawu SDK platformy Azure można określić w pliku diagnostics.wadcfgx hello hello konta magazynu.

> [!NOTE]
> Te instrukcje mają zastosowanie tylko tooAzure 2.4 zestawu SDK i poniżej. Dla 2.5 zestawu SDK platformy Azure można określić w pliku diagnostics.wadcfgx hello hello konta magazynu.
>
>

Parametry połączenia hello tooset:

1. Otwórz plik ServiceConfiguration.Cloud.cscfg hello przy użyciu ulubionym edytorze tekstów i parametry połączenia hello zestaw magazynu. Witaj *AccountName* i *AccountKey* wartości znajdują się w hello portalu Azure w hello konta pulpitu nawigacyjnego magazynu, w obszarze klucze dostępu.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Zapisz plik ServiceConfiguration.Cloud.cscfg hello.
3. Otwórz plik ServiceConfiguration.Local.cscfg hello i sprawdź, czy UseDevelopmentStorage jest ustawiony tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Teraz, gdy parametry połączenia hello są ustawione, aplikacji zachować konta magazynu tooyour danych diagnostycznych, po wdrożeniu aplikacji.
4. Zapisz i skompilowanie projektu, a następnie wdrożyć aplikację.

## <a name="step-2-optional-create-custom-performance-counters"></a>Krok 2: (Opcjonalnie) Utwórz niestandardowe liczniki wydajności
Ponadto toohello wstępnie zdefiniowana liczniki wydajności, można dodawać role sieci web lub procesu roboczego toomonitor liczników wydajności niestandardowych. Niestandardowe liczniki wydajności mogą być używane tootrack i monitorowanie zachowania specyficzne dla aplikacji i można utworzyć lub usunąć zadanie uruchamiania, rola sieci web lub roli proces roboczy z podwyższonym poziomem uprawnień.

agent Azure diagnostics Hello odświeża hello konfigurację liczników wydajności z pliku .wadcfg hello minutę po uruchomieniu.  Utwórz niestandardowe liczniki wydajności w hello — metoda OnStart, uruchamiania zadań trwać dłużej niż minutę tooexecute Twoje niestandardowe liczniki wydajności będą nie została utworzona podczas agenta diagnostyki Azure hello tooload je.  W tym scenariuszu zobaczysz, że diagnostyki Azure poprawnie przechwytuje wszystkie dane diagnostyczne, z wyjątkiem Twojego niestandardowe liczniki wydajności.  tooresolve ten problem, Utwórz hello liczników wydajności w zadanie uruchamiania lub Przenieś niektóre zadania uruchamiania działają — metoda OnStart toohello po utworzeniu hello liczników wydajności.

Wykonaj następujące kroki toocreate proste wydajności niestandardowych licznik o nazwie "\MyCustomCounterCategory\MyButton1Counter" hello:

1. Otwórz plik definicji usługi hello (CSDEF) dla aplikacji.
2. Dodaj hello środowiska uruchomieniowego element toohello sieć Web lub proces roboczy elementu tooallow wykonywania z podwyższonym poziomem uprawnień:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Zapisz plik hello.
4. Otwórz plik diagnostyki hello (diagnostics.wadcfg w 2.4 zestawu SDK i poniżej lub diagnostics.wadcfgx w zestawie SDK, 2.5 lub nowszym) i dodaj następujące toohello DiagnosticMonitorConfiguration hello

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Zapisz plik hello.
6. Utwórz kategorii licznika wydajności niestandardowych hello w — metoda OnStart hello swojej roli przed wywołaniem base. OnStart. Witaj poniższy przykład C# tworzy kategorię niestandardową, jeśli jeszcze nie istnieje:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Aktualizuj liczniki hello w aplikacji. Poniższy przykład Hello aktualizacje licznika wydajności niestandardowych zdarzeń Button1_Click:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Zapisz plik hello.  

Dane licznika wydajności niestandardowych teraz zostaną zebrane przez monitor diagnostyki Azure hello.

## <a name="step-3-query-performance-counter-data"></a>Krok 3: Wykonywanie zapytań danych licznika wydajności
Po wdrożeniu aplikacji i uruchomiona, monitor diagnostyki hello rozpocznie się zbierania liczników wydajności i przechowywanie tego tooAzure pamięci masowej. Użyj narzędzi takich jak Eksplorator serwera w programie Visual Studio, [Eksploratora usługi Storage Azure](http://azurestorageexplorer.codeplex.com/), lub [Menedżera diagnostyki Azure](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) przez Cerebrata danych w hello liczniki wydajności hello tooview Tabela WADPerformanceCountersTable. Można również programowo zapytania przy użyciu usługi tabeli hello [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), lub [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hello poniższy przykład C# zawiera podstawowe zapytanie tabeli WADPerformanceCountersTable hello i zapisuje plik CSV tooa hello diagnostyki danych. Po hello liczniki wydajności zostaną zapisane w pliku CSV tooa, można użyć hello Tworzenie wykresów możliwości programu Microsoft Excel lub pewne inne narzędzie toovisualize hello dane. Należy się tooadd tooMicrosoft.WindowsAzure.Storage.dll odwołania, który jest dostępny w hello Azure SDK dla platformy .NET października 2012 lub nowszy. zestaw Hello jest zainstalowana toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ katalogu.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Jednostki są mapowane tooC # obiektów za pomocą niestandardowej klasy pochodzącej od **TableEntity**. Witaj poniższy kod definiuje klasę jednostki, która reprezentuje licznika wydajności w hello **WADPerformanceCountersTable** tabeli.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Następne kroki
[Przeglądanie dodatkowych artykułów na diagnostyki Azure](../azure-diagnostics.md)
