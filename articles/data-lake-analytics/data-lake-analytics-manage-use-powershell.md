---
title: "aaaManage Azure Data Lake Analytics przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania konta usługi Data Lake Analytics toomanage, źródła danych i elementy katalogu. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Dowiedz się, jak zadania konta usługi Azure Data Lake Analytics toomanage, źródeł danych, a elementami katalogu przy użyciu programu Azure PowerShell. 

## <a name="prerequisites"></a>Wymagania wstępne

Po utworzeniu konta usługi Data Lake Analytics należy tooknow:

* **Identyfikator subskrypcji**: hello identyfikator subskrypcji platformy Azure, pod którym znajduje się konto usługi Data Lake Analytics.
* **Grupa zasobów**: hello nazwę grupy zasobów platformy Azure hello, która zawiera konto usługi Data Lake Analytics.
* **Nazwa konta usługi Data Lake Analytics**: hello konta Nazwa może zawierać tylko małe litery i cyfry.
* **Domyślne konto usługi Data Lake Store**: każde konto usługi Data Lake Analytics ma domyślne konto usługi Data Lake Store. Te konta należy hello tej samej lokalizacji.
* **Lokalizacja**: hello lokalizacji konta usługi Data Lake Analytics, takie jak "Wschodnie stany USA 2" lub inne obsługiwane lokalizacje. Obsługiwane lokalizacje będą widoczne na naszych [cennikiem](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

Witaj wstawki programu PowerShell w tym samouczku te informacje służą toostore tych zmiennych

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Logowanie się

Zaloguj się za pomocą identyfikatora subskrypcji.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Zaloguj się za pomocą nazwę subskrypcji.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Witaj `Login-AzureRmAccount` polecenia cmdlet zawsze wyświetla monit o podanie poświadczeń. Można uniknąć monitowania za pomocą następującego polecenia cmdlet hello:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Zarządzanie kontami

### <a name="create-a-data-lake-analytics-account"></a>Tworzenie konta Data Lake Analytics

Jeśli nie masz jeszcze [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, utwórz je. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Każde konto usługi Data Lake Analytics wymaga domyślnego konta usługi Data Lake Store używanego do przechowywania dzienników. Można ponownie użyć istniejącego konta lub utworzyć konto. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Gdy grupa zasobów i konto magazynu usługi Data Lake Store będą dostępne, utwórz konto usługi Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Uzyskiwanie informacji o koncie

Uzyskiwanie szczegółowych informacji o koncie.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Sprawdź hello istnienie określonego konta usługi Data Lake Analytics. polecenie cmdlet Hello zwraca albo `True` lub `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Sprawdź hello istnienie określonego konta usługi Data Lake Store. polecenie cmdlet Hello zwraca albo `True` lub `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Wyświetlanie listy kont

Lista Data Lake Analytics kont w obrębie hello bieżącej subskrypcji.

```powershell
Get-AdlAnalyticsAccount
```

Lista Data Lake Analytics kont w ramach określonej grupy zasobów.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Zarządzanie regułami zapory

Lista reguł zapory.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Dodaj regułę zapory.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Zmień reguły zapory.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Usuń regułę zapory.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Zezwalaj na adresy IP platformy Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Zarządzanie źródłami danych
Azure Data Lake Analytics obsługuje obecnie hello następujące źródła danych:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Podczas tworzenia konta usługi Analytics należy wyznaczyć usługi Data Lake Store konta toobe hello domyślne źródło danych. Witaj domyślnego konta usługi Data Lake Store służy toostore zadania metadanych i zadania dziennika inspekcji. Po utworzeniu konta usługi Data Lake Analytics można dodać dodatkowe konta usługi Data Lake Store i/lub konta magazynu. 

### <a name="find-hello-default-data-lake-store-account"></a>Znajdź hello domyślnego konta usługi Data Lake Store

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Można znaleźć hello domyślnego konta usługi Data Lake Store za pomocą filtrowania hello lista źródeł danych chronionych przez hello `IsDefault` właściwości:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Dodawanie źródła danych

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Lista źródeł danych

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Przesyłanie zadań U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Przedstawia ciąg jako skrypt U-SQL

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a>Przesyłanie pliku jako skrypt U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Lista zadania konta

### <a name="list-all-hello-jobs-in-hello-account"></a>Listę wszystkich zadań hello w hello konta. 

dane wyjściowe Hello zawierają hello aktualnie uruchomione zadania i zadania, które zostały ostatnio wykonane.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Lista określoną liczbę zadań

Domyślnie jest sortowana hello listy zadań na czas przesyłania. Dlatego hello ostatnio przesłane zadania występować jako pierwszy. Domyślnie program hello konta ADLA pamięta zadania na okres 180 dni, ale polecenia cmdlet hello Ge AdlJob przez domyślny zwraca hello tylko 500 pierwszych. Użyj - Top parametru toolist określoną liczbę zadań.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Lista zadań na podstawie wartości hello właściwości zadania

Przy użyciu hello `-State` parametru. Możesz połączyć ze sobą następujące wartości:

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

Użyj hello `-Result` toodetect parametru czy zakończonych zadań została ukończona pomyślnie. Ma ona następujące wartości:

* Anulowane
* Nie powiodło się
* Brak
* Powodzenie

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Witaj `-Submitter` parametru pomagają określić, kto przesłać zadania.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Witaj `-SubmittedAfter` jest przydatny do filtrowania tooa zakresu czasu.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Typowe scenariusze dotyczące wyświetlania zadań


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a>Filtrowanie listy zadań

Po utworzeniu listy zadań w bieżącej sesji programu PowerShell. Można użyć normalnej listy hello toofilter poleceń cmdlet programu PowerShell.

Filtr listy zadań toohello zadania przesłane w hello ostatnich 24 godzinach

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filtrowanie listy zadań toohello zadania, które zostało zakończone w hello w ostatnich 24 godzinach

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filtrowanie listy zadań toohello zadania, które uruchomienia. Zadania może się nie powieść w czasie kompilacji - i dlatego nigdy nie uruchamia. Przyjrzyjmy się zadania hello nie powiodło się, które faktycznie uruchomienia, a następnie nie powiodło się.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Analizowanie listy zadań

Użyj hello `Group-Object` tooanalyze polecenia cmdlet listy zadań.

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
Podczas przeprowadzania analizy, może to być przydatne tooadd właściwości toohello zadania obiektów toomake filtrowania i grupowania prostsze. powitania po fragment kodu przedstawia obliczania tooannotate a informacji o zadaniu z właściwości.

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a>Pobieranie informacji o potoki i powtórzeń

Użyj hello `Get-AdlJobPipeline` polecenia cmdlet toosee hello potoku informacji wcześniej zgłoszonych zadania.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Użyj hello `Get-AdlJobRecurrence` informacje o cyklu hello toosee polecenia cmdlet dla poprzednio przesłany zadań.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Pobierz informacje o zadaniu

### <a name="get-job-status"></a>Pobierz stan zadania

Pobierz stan hello danego zadania.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Sprawdź dane wyjściowe zadania hello

Po zakończeniu zadania hello, sprawdź, czy plik wyjściowy hello istnieje poprzez wyszczególnienie hello pliki w folderze.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Zarządzanie uruchomionych zadań

### <a name="cancel-a-job"></a>Anulowanie zadania

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Poczekaj, aż toofinish zadania

Zamiast powtarzające się `Get-AdlAnalyticsJob` zakończenie zadania można użyć hello `Wait-AdlJob` toowait polecenia cmdlet dla hello tooend zadania.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Zarządzanie zasadami obliczeń

### <a name="list-existing-compute-policies"></a>Wyświetl listę istniejących zasad obliczeń

Witaj `Get-AdlAnalyticsComputePolicy` polecenie cmdlet pobiera informacje o zasadach obliczeniowe dla konta usługi Data Lake Analytics.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Tworzenie zasad obliczeń

Witaj `New-AdlAnalyticsComputePolicy` polecenie cmdlet tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics. W przykładzie zestawy hello maksymalna toohello dostępne AUs określony too50 użytkownika i too250 priorytet zadania minimalna hello.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Sprawdź, czy istnieje plik hello.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Przekazywanie i pobieranie

Przekaż plik.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Przekaż rekursywnie całego folderu.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Pobierz plik.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Pobierz rekursywnie całego folderu.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Jeśli hello przekazać lub proces pobierania zostanie przerwany, możesz spróbować tooresume hello procesu uruchomionego cmdlet hello ponownie z hello ``-Resume`` flagi.

## <a name="manage-catalog-items"></a>Zarządzanie elementów katalogu

wykaz Hello U-SQL jest toostructure używanych danych i kod, aby mogły być udostępniane przez skrypty U-SQL. wykaz Hello umożliwia hello najwyższym możliwym poziomie wydajności z danymi w usłudze Azure Data Lake. Więcej informacji znajduje się w temacie [Używanie katalogu U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Elementy listy w katalogu hello U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Wyświetl listę wszystkich zestawów hello w wszystkich hello baz danych na koncie ADLA.

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a>Uzyskiwanie szczegółowych informacji o elemencie katalogu

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Utwórz poświadczenia w katalogu

W bazie danych U-SQL Utwórz obiekt poświadczeń dla bazy danych hostowanej na platformie Azure. Obecnie U-SQL poświadczenia są jedynym typem hello elementu katalogu, który można utworzyć za pomocą programu PowerShell.

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a>Uzyskać podstawowe informacje o koncie ADLA

Wyszukuje określoną nazwę konta, podstawowe informacje o koncie hello hello następującego kodu

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a>Praca z platformy Azure

### <a name="get-details-of-azurerm-errors"></a>Uzyskiwanie szczegółowych informacji o błędach AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Sprawdź, czy są uruchomione jako administrator

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Znajdowanie identyfikatora dzierżawcy

Na podstawie nazwy subskrypcji:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

Z identyfikatorem subskrypcji:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

Z adresu domeny, takie jak "contoso.com"


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Wyświetl listę wszystkich subskrypcji i dzierżawców identyfikatorów

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Utwórz konto usługi Data Lake Analytics przy użyciu szablonu

Można także użyć szablonu grupy zasobów platformy Azure przy użyciu hello następującego skryptu programu PowerShell:

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

Aby uzyskać więcej informacji, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) i [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Przykład szablonu**

Zapisz hello następującego tekstu jako tekstu zawierającego `.json` pliku, a następnie użyj hello poprzedzających szablonu hello toouse skrypt programu PowerShell. 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* Wprowadzenie do usługi Data Lake Analytics przy użyciu [portalu Azure](data-lake-analytics-get-started-portal.md) | [programu Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [2.0 interfejsu wiersza polecenia](data-lake-analytics-get-started-cli2.md)
* Zarządzanie usługą Azure Data Lake Analytics przy użyciu [portalu Azure](data-lake-analytics-manage-use-portal.md) | [programu Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [interfejsu wiersza polecenia](data-lake-analytics-manage-use-cli.md) 
