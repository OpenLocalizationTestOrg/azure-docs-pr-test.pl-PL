---
title: "Środowiska PowerShell: Tworzenie i zarządzanie puli elastycznej Azure SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PowerShell toomanage puli elastycznej."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Tworzenie i zarządzanie nimi przy użyciu programu PowerShell puli elastycznej
W tym temacie opisano sposób toocreate i zarządzanie nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) przy użyciu programu PowerShell.  Można również utworzyć i zarządzać nimi puli elastycznej platformy Azure przy użyciu hello [portalu Azure](https://portal.azure.com/), interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md). Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Tworzenie puli elastycznej
Witaj [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) polecenie cmdlet tworzy puli elastycznej. Witaj wartości jednostek eDTU na pulę oraz minimalne i maksymalne liczby jednostek Dtu są ograniczone przez wartość warstwy usługi hello (Basic, Standard, Premium lub Premium RS). Zobacz [limity liczby jednostek eDTU i Magazyn puli baz danych i pul elastycznych](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Tworzenie puli bazy danych w puli elastycznej
Użyj hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) polecenia cmdlet i zestaw hello **ElasticPoolName** parametru toohello docelową pulę. Zobacz toomove istniejącej bazy danych w puli elastycznej [przenieść bazę danych w puli elastycznej](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Kompletny skrypt
Ten skrypt tworzy grupę zasobów platformy Azure i serwer. Po wyświetleniu monitu podaj nazwę użytkownika administratora i hasło hello nowego serwera (inne niż poświadczenia Azure).

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Tworzenie puli elastycznej i dodawanie wielu baz danych w puli
Tworzenie wielu baz danych w puli elastycznej może trwać, jeśli odbywa się za pomocą portalu hello lub poleceń cmdlet programu PowerShell, który tworzenie tylko jednej bazy danych w czasie. Tworzenie tooautomate w puli elastycznej, zobacz [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Przenoszenie bazy danych w puli elastycznej
Można przenieść bazę danych do lub z puli elastycznej z hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Zmień ustawienia wydajności puli elastycznej
Gdy wystąpi wydajności, możesz zmienić ustawienia hello hello puli tooaccommodate przyrostu. Użyj hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) polecenia cmdlet. Ustaw hello - Dtu parametru toohello Edtu na pulę. Zobacz [limity liczby jednostek eDTU i magazyn](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) prawidłowych wartości.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Zmień hello limit magazynu elastycznej puli

Użyj hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) hello tooset polecenia cmdlet _- StorageMB_ parametru. Podaj hello limit magazynu w Megabajtach (na przykład 2097152 zestawy hello magazynu limit too2 TB). Zobacz [limity liczby jednostek eDTU i magazyn](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) prawidłowych wartości.

> [!IMPORTANT]
> Hello domyślny maksymalny pamięci masowej na pulę dla pul Premium z Edtu 1500 lub więcej jest 750 GB. wyższy hello tooobtain _maksymalny rozmiar magazynu danych na pulę_, hello limit magazynu musi być wyraźnie ustawione. Pule Premium z więcej niż 750 GB przestrzeni dyskowej jest obecnie w wersji zapoznawczej w następujących regionach hello: wschodnie stany USA 2, zachodnie stany USA Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Niemcy centralnej, Azja południowo-wschodnia, Japonia Wschodnia, Australia Wschodnia, centralnej Zjednoczone i Kanada Wschodnia.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Pobierz stan hello operacji puli
Tworzenie puli elastycznej może potrwać. Stan hello tootrack operacji puli, w tym tworzenia i aktualizacji, użyj hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) polecenia cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Pobierz stan hello przenoszenia bazy danych do i z puli elastycznej
Przenoszenie bazy danych może potrwać. Śledzenie stanu przenoszenia przy użyciu hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) polecenia cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Pobierz dane o użyciu zasobów dla puli elastycznej
Metryki, które mogą być pobierane w procentach limit puli zasobów hello:

| Nazwa metryki | Opis |
|:--- |:--- |
| Procesor CPU\_procent |Średnia obliczeniowe wykorzystania w procentach limit hello hello puli. |
| fizyczny\_danych\_odczytu\_procent |Średnie wykorzystanie we/wy w procent opartych na powitania limit hello puli. |
| Dziennik\_zapisu\_procent |Średnia zapisu wykorzystania zasobów w procentach limit hello hello puli. |
| DTU\_zużycie\_procent |Użycie średnią liczbę jednostek eDTU w procentach limit liczby jednostek eDTU puli hello |
| Magazyn\_procent |Średnie wykorzystanie magazynu w procentach hello limit magazynowania puli hello. |
| Pracownicy\_procent |Maksymalna równoczesnych pracowników (liczba żądań) procent opartych na powitania limit hello puli. |
| sesje\_procent |Maksymalna liczba sesji jednoczesnych wyrażony jako procent oparte na powitania limit hello puli. |
| eDTU_limit |Bieżący maksymalny puli elastycznej jednostek dtu w warstwie ustawienie dla tej puli elastycznej w danym przedziale czasu. |
| Magazyn\_limit |Bieżący limit magazynowania puli elastycznej max ustawienie dla tej elastycznej puli w megabajtach w danym przedziale czasu. |
| eDTU\_używane |Średnia Edtu użytej przez pulę hello w tym zakresie. |
| Magazyn\_używane |Średni Magazyn używany przez pulę hello w tym interwał, w bajtach |

**Okresy przechowywania/szczegółowości metryki:**

* Dane są zwracane w szczegółowości 5 minut.  
* Przechowywanie danych jest 35 dni.  

To polecenie cmdlet i interfejsu API ogranicza hello liczbę wierszy, które mogą być pobierane w jednym wywołaniu too1000 wierszy (około 3 dni dane o 5 minut). To polecenie można wywoływać wielokrotnie tooretrieve przedziały czasu rozpoczęcia/zakończenia różnych większej ilości danych, ale

metryki hello tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Pobierz dane o użyciu zasobów dla bazy danych w puli elastycznej
Te interfejsy API są tak samo jak hello interfejsy API używane do monitorowania wykorzystania zasobów hello jednej bazy danych, z wyjątkiem powitania po semantycznego różnica hello: metryki pobierane są wyrażone jako procent hello na Edtu max bazy danych (lub równoważne zakończenia dla hello bazowy metryki, takie jak procesor CPU lub we/wy) ustawić dla tej puli. Na przykład 50% wykorzystania któregokolwiek z tych metryk wskazuje, że zużycie zasobów specyficznych hello jest na 50% hello limitu zakończenia bazy danych dla tego zasobu w puli nadrzędnej hello.

metryki hello tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Dodaj zasób puli elastycznej tooan alertu
Można dodać reguły alertów toosend puli elastycznej tooan wiadomości e-mail z powiadomieniami lub zbyt alert parametry[adres URL punktów końcowych](https://msdn.microsoft.com/library/mt718036.aspx) po puli elastycznej hello trafienia ustawiony próg użycia. Użyj polecenia cmdlet hello AzureRmMetricAlertRule Dodaj.

> [!IMPORTANT]
> Monitorowanie dla pul elastycznych wykorzystania zasobów ma opóźnienie co najmniej 5 minut. Ustawianie alertów mniej niż 10 minut pule elastyczne nie jest obecnie obsługiwane. Ustaw alerty dla pul elastycznych kropką (parametr o nazwie "-Rozmiar_okna" w interfejsie API środowiska PowerShell) mniej niż 10 minut mogą nie zostać wyzwolone. Upewnij się, że wszystkie alerty zdefiniowane dla pul elastycznych użyć ciągu (rozmiar okna) 10 minut lub więcej.
>
>

W tym przykładzie dodaje alert w przypadku uzyskiwania powiadomienia, gdy użycie jednostek eDTU puli elastycznej wykraczają poza pewnej wartości progowej.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Dodawanie baz danych tooall alertów w puli elastycznej
Można dodać reguły alertów tooall toosend puli elastycznej bazy danych wiadomości e-mail z powiadomieniami lub zbyt alert parametry[adres URL punktów końcowych](https://msdn.microsoft.com/library/mt718036.aspx) gdy zasób trafienia wartość progową wykorzystania przez hello alertu.

> [!IMPORTANT]
> Monitorowanie dla pul elastycznych wykorzystania zasobów ma opóźnienie co najmniej 5 minut. Ustawianie alertów mniej niż 10 minut pule elastyczne nie jest obecnie obsługiwane. Ustaw alerty dla pul elastycznych kropką (parametr o nazwie "-Rozmiar_okna" w interfejsie API środowiska PowerShell) mniej niż 10 minut mogą nie zostać wyzwolone. Upewnij się, że wszystkie alerty zdefiniowane dla pul elastycznych użyć ciągu (rozmiar okna) 10 minut lub więcej.
>

W tym przykładzie dodaje alertu tooeach hello baz danych w puli elastycznej dla pobierania powiadomienie, gdy użycie jednostek DTU w tej bazie danych przekracza określony próg.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Zbieranie i monitorować dane użycia zasobów przez wiele pul w ramach subskrypcji
Jeśli masz wiele baz danych w ramach subskrypcji jest skomplikowane toomonitor każdego elastyczna pula oddzielnie. Zamiast tego polecenia cmdlet programu PowerShell bazy danych SQL i zapytania T-SQL mogą być połączone toocollect dane o użyciu zasobów z wielu zestawów i ich baz danych monitorowania i analizy użycia zasobów. A [przykładowe zastosowanie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) zestawu powershell skryptów znajdują się w repozytorium przykłady GitHub programu SQL Server hello wraz z dokumentacją na działanie i w jaki sposób toouse go.

toouse przykładowe zastosowanie, wykonaj następujące kroki.

1. Pobierz hello [skrypty i dokumentacja](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Zmodyfikuj skrypty hello w danym środowisku. Określ co najmniej jeden serwer, na których znajdują się elastyczne pule.
3. Określ bazę danych telemetrii, gdzie hello zebranych metryk są toobe przechowywane.
4. Dostosowywanie hello skryptu toospecify hello czas trwania wykonywanie skryptów hello.

Na wysokim poziomie skrypty hello hello następujące:

* Wylicza wszystkie serwery w ramach danej subskrypcji Azure (lub określona lista serwerów).
* Uruchamia zadanie w tle dla każdego serwera. zadanie Hello jest uruchamiany w pętli w regularnych odstępach czasu i zbiera dane telemetryczne dla wszystkich pul hello w powitania serwera. Następnie ładuje hello zbierane dane do bazy danych telemetrii określonego hello.
* Wylicza listę baz danych w każdej puli toocollect hello bazy danych dane o użyciu zasobów. Następnie ładuje hello zbierane dane do bazy danych telemetrycznych hello.

Hello zebranych metryk w bazie danych telemetrycznych hello mogą być przeanalizowane toomonitor hello kondycji pule elastyczne i baz danych hello w nim. skrypt Hello instaluje również wstępnie zdefiniowane wartościami przechowywanymi w tabeli funkcji (TVF) w metryki bazy danych telemetrii hello agregacji hello toohelp okna określony czas. Na przykład wyniki hello funkcji TVF mogą być używane tooshow "pierwszych N pule elastyczne z hello wykorzystania maksymalną liczbę jednostek eDTU w danym momencie oknie." Opcjonalnie użyj narzędzia analityczne, takie jak tooquery programu Excel lub Power BI i analizować dane zbierane hello.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Przykład: pobieranie metryk zużycia zasobów dla puli elastycznej i jej baz danych
W tym przykładzie pobierana hello zużycie metryki dla danej puli elastycznej i jej baz danych. Zebrane dane jest sformatowany i zapisywane sformatowanym plikiem CSV tooa. Plik Hello można przeglądać przy użyciu programu Excel.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>Czas oczekiwania operacji puli elastycznej
* Zmiana hello minimalna liczba jednostek Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.
* Zmiana hello Edtu na pulę, zależy od hello łączną ilość miejsca używanego przez wszystkie bazy danych w puli hello. Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB. Na przykład jeśli całkowita ilość miejsca hello jest używany przez wszystkie bazy danych w puli hello jest 200 GB, a następnie hello oczekuje się, że czas oczekiwania na zmianę hello puli eDTU na pulę wynosi 3 godziny lub mniej.



## <a name="next-steps"></a>Następne kroki
* [Tworzenie zadań elastycznych](sql-database-elastic-jobs-overview.md) zadania elastyczne umożliwiają uruchamianie skryptów T-SQL na dowolnej liczbie baz danych w puli hello.
* Zobacz [skalowanie w poziomie z bazy danych SQL Azure](sql-database-elastic-scale-introduction.md): Użyj narzędzi elastycznej tooscale wychodzących, przenoszenia danych, zapytania, lub utworzyć transakcji.
