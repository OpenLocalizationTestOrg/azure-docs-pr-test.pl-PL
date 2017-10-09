---
title: metryki magazynu aaaEnabling w hello portalu Azure | Dokumentacja firmy Microsoft
description: "Jak metryki magazynu tooenable hello usług obiektów Blob, kolejki, tabel i plików"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Włączanie metryk magazynu i wyświetlanie danych metryk
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Omówienie
Metryki magazynu jest domyślnie włączona, podczas tworzenia nowego konta magazynu. Można skonfigurować monitorowanie za pomocą obu hello [klasycznego portalu Azure](https://manage.windowsazure.com), środowiska Windows PowerShell lub programistycznie za pośrednictwem interfejsu API magazynu.

Po włączeniu metryki magazynu, musisz wybrać okres przechowywania danych hello: tego okresu określa, jak długo magazynu hello usługi śledzi hello metryki i opłat za hello miejsce wymagane toostore je. Zwykle należy używać krótszy okres przechowywania dla metryki minuty niż metryki co godzinę z powodu hello znaczących dodatkowe miejsce wymagane dla metryki minuty. Okres przechowywania należy wybrać w taki sposób, że mają wystarczającą ilość czasu tooanalyze hello danych i Pobierz wszystkie metryki mają tookeep dla celów raportowania analizy offline lub. Należy pamiętać, że opłaty będą również naliczane pobierania danych metryki z konta magazynu.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Jak przy użyciu metryk Storage tooenable hello klasycznego portalu Azure
W hello [klasycznego portalu Azure](https://manage.windowsazure.com), użyj hello strony konfiguracji dla toocontrol konta magazynu metryki magazynu. Do monitorowania, można ustawić poziomu i okres przechowywania w dniach dla każdego z obiektów blob, tabel i kolejek. W każdym przypadku poziom hello jest jedną z następujących hello:

* OFF — Nie zebrano żadnych metryki.
* Minimalnie — Podstawowy zestaw metryk, takich jak wejście/wyjście, dostępności, opóźnienia i procent powodzenia, które są agregowane dla usług obiektów Blob, tabel i kolejek hello zbiera metryki magazynu.
* Verbose — Zbiera metryki magazynu cały zestaw miar, który zawiera hello same metryki dla każdej operacji interfejsu API magazynu, oprócz toohello poziomu usług metryki. Pełne metryki Włącz analizę bliżej problemów występujących podczas działania aplikacji.

Należy pamiętać, że hello klasycznego portalu Azure nie obecnie obsługuje tooconfigure minuty metryki na koncie magazynu; należy włączyć metryki minuty przy użyciu programu PowerShell lub programowo.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Jak tooenable metryki magazynu przy użyciu programu PowerShell
W systemie PowerShell tooconfigure Twojego komputera lokalnego magazynu metryki na koncie magazynu przy użyciu hello Azure PowerShell polecenia cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello bieżące ustawienia i hello polecenia cmdlet Zestaw AzureStorageServiceMetricsProperty toochange hello bieżące ustawienia.

polecenia cmdlet Hello, określające metryki magazynu używają hello następujące parametry:

* MetricsType możliwe wartości to godziny i minuty.
* Typ ServiceType możliwe wartości to obiektów Blob, kolejki i tabeli.
* MetricsLevel możliwe wartości to None (równoważne tooOff w hello klasycznego portalu Azure), usługa (równoważne tooMinimal w hello klasycznego portalu Azure) i ServiceAndApi (równoważne tooVerbose w hello klasycznego portalu Azure).

Na przykład hello następujące polecenie zmienia na minutę metryki dla usługi blob hello w domyślne konto magazynu z okresu przechowywania hello ustawić toofive dni:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
Witaj następujące polecenie pobiera hello bieżącego co godzinę metryki poziomu i przechowywania dni hello usługi obiektów blob na koncie magazynu domyślne:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
Aby dowiedzieć się jak tooconfigure hello Azure PowerShell polecenia cmdlet toowork z subskrypcją platformy Azure oraz jak tooselect hello magazynu domyślnego konta toouse, zobacz: [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Jak tooenable metryki magazynu programowo
powitania po fragment kodu C# pokazano, jak metryki tooenable i rejestrowanie przy użyciu usługi Blob hello hello biblioteki klienta usługi storage dla platformy .NET:

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Wyświetlanie metryki magazynu
Po skonfigurowaniu magazynu metryki toomonitor Twojego konta magazynu, rejestruje metryki hello w zestawie dobrze znanego tabel na koncie magazynu. Strona Monitor hello służy dla konta magazynu w hello metryki co godzinę hello tooview klasycznego portalu Azure udostępnianymi na wykresie. Na tej stronie powitania klasycznego portalu Azure możesz:

* Wybierz tooplot metryk, które na wykresie hello (wybór hello dostępne metryki zależy od tego, czy została wybrana opcja pełne lub minimalnym monitorowania usługi hello na stronie Konfiguruj hello).
* Wybierz zakres czasu hello hello metryki wyświetlane na wykresie hello.
* Wybierz toouse metryki hello tooplot skali bezwzględny lub względny.
* Konfigurowanie poczty e-mail alertów toonotify podczas określonej metryki osiąga określoną wartość.

Jeśli chcesz toodownload hello metryki dla magazynu długoterminowego lub tooanalyze je lokalnie, będzie konieczne toouse narzędzia lub pisania kodu tooread hello tabel. Należy pobrać hello minuty metryki dla analizy. tabele Hello nie jest wyświetlana lista wszystkich tabel hello na koncie magazynu, ale można go wywołać bezpośrednio przez nazwę. Wiele firm Przeglądanie magazynu narzędzi potrafią zidentyfikować te tabele i pozwala tooview je bezpośrednio (zobacz hello blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę dostępnych narzędzi).

### <a name="hourly-metrics"></a>Metryki co godzinę
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Metryki minuty
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Pojemność
* $MetricsCapacityBlob

Dla tych tabel w można znaleźć szczegółowe informacje dotyczące schematów hello [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/azure/hh343264.aspx). Poniższe wiersze próbki Hello Pokaż tylko podzestaw kolumn hello jest dostępne, ale zilustrować niektóre ważne funkcje sposób hello metryki magazynu zapisuje te metryki:

| PartitionKey | RowKey | Znacznik czasu | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Dostępność | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |Użytkownik; Wszystkie |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |Użytkownik; QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |Użytkownik; QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |Użytkownik; UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

W przykładowe dane metryk minuty klucza partycji hello używany czas hello rozdzielczością minuty. klucz wiersza Hello identyfikuje hello typ informacji przechowywanych w wierszu hello i składa się z dwóch części informacji, typ dostępu hello i typ żądania hello:

* Typ dostępu Hello jest użytkownika lub systemu, gdzie usługa Magazyn toohello żądań użytkownika tooall odwołuje się użytkownika, a system odwołuje się toorequests przez analityka magazynu.
* Typ żądania Hello jest w takim przypadku jest to wiersz podsumowania, lub identyfikuje hello określonego interfejsu API, takich jak QueryEntity lub UpdateEntity.

rekordy danych przykładowych Hello powyżej pokazuje wszystkie hello na minutę (rozpoczyna się od 11:00:00), tak hello liczba żądań QueryEntities plus hello liczba żądań QueryEntity plus hello liczba żądań UpdateEntity sumują tooseven, który jest hello całkowita wyświetlany na Witaj użytkownika: wierszy. Podobnie, mogą pochodzić hello średnie opóźnienie end-to-end 104.4286 w wierszu użytkownika: All hello obliczając ((143.8 * 5) + 3 + 9) / 7.

Konfigurowanie alertów w hello klasycznego portalu Azure na stronie Monitor hello należy rozważyć, aby metryki magazynu można automatycznie powiadamia użytkownika o wszelkich ważne zmiany w zachowaniu hello usług magazynu. Jeśli używasz toodownload narzędzie Eksploratora magazynu te dane metryk w formacie rozdzielanym, można użyć programu Microsoft Excel tooanalyze hello danych. Zobacz hello blogu [eksploratory usługi Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) listę narzędzi Eksploratora dostępny magazyn.

## <a name="accessing-metrics-data-programmatically"></a>Uzyskiwanie dostępu do danych metryki programowo
Hello poniżej zawiera przykładowe C# kod, który uzyskuje dostęp do hello minuty metryki dla zakresu minut i wyświetla wyniki hello w okna konsoli. Używa ona hello biblioteki usługi Azure Storage w wersji 4 zawierającą hello CloudAnalyticsClient klasy, które upraszcza podczas uzyskiwania dostępu do tabel metryki hello w magazynie.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Jakie opłat ponosisz po włączeniu metryki magazynu?
Zapis jednostek tabeli toocreate żądania dla metryki są naliczane według hello stawki standardowe tooall dotyczy usługi Azure Storage operacji.

Żądania odczytu i usuwania danych toometrics klienta są również rozliczeniowy stawkami standardowymi. Jeśli zostały skonfigurowane zasady przechowywania danych, nie są naliczane gdy magazyn Azure usuwa stare dane metryk. Jeśli usuniesz dane analityczne, Twoje konto jest pobierana dla operacji delete hello.

pojemność Hello używane przez hello metryki tabel jest również rozliczeniowy: można użyć powitania po tooestimate hello ilość wydajności używany do przechowywania danych metryki:

* Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 148KB danych jest przechowywana co godzinę w tabelach transakcji metryki powitania po włączeniu zarówno usługi, jak i interfejs API na poziomie podsumowania.
* Jeśli co godzinę usługa korzysta z każdego interfejsu API w każdej usługi, następnie 12KB danych jest przechowywana co godzinę w tabelach transakcji metryki hello włączenie tylko poziom usługi podsumowania.
* Witaj pojemności tabeli obiektów blob ma dwa wiersze dodane każdego dnia (zakładając, że użytkownik wybrał w dzienników): oznacza to, że każdy dzień hello rozmiar tej tabeli zwiększa się tooapproximately 300 bajtów.

## <a name="next-steps"></a>Następne kroki:
[Włączanie analityka magazynu, rejestrowania i uzyskiwanie dostępu do danych dziennika](https://msdn.microsoft.com/library/dn782840.aspx)
