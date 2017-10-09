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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="0aa70-103">Zarządzanie usługą Azure Data Lake Analytics przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0aa70-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="0aa70-104">Dowiedz się, jak zadania konta usługi Azure Data Lake Analytics toomanage, źródeł danych, a elementami katalogu przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aa70-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0aa70-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0aa70-105">Prerequisites</span></span>

<span data-ttu-id="0aa70-106">Po utworzeniu konta usługi Data Lake Analytics należy tooknow:</span><span class="sxs-lookup"><span data-stu-id="0aa70-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="0aa70-107">**Identyfikator subskrypcji**: hello identyfikator subskrypcji platformy Azure, pod którym znajduje się konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="0aa70-108">**Grupa zasobów**: hello nazwę grupy zasobów platformy Azure hello, która zawiera konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="0aa70-109">**Nazwa konta usługi Data Lake Analytics**: hello konta Nazwa może zawierać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="0aa70-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="0aa70-110">**Domyślne konto usługi Data Lake Store**: każde konto usługi Data Lake Analytics ma domyślne konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0aa70-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="0aa70-111">Te konta należy hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0aa70-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="0aa70-112">**Lokalizacja**: hello lokalizacji konta usługi Data Lake Analytics, takie jak "Wschodnie stany USA 2" lub inne obsługiwane lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="0aa70-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="0aa70-113">Obsługiwane lokalizacje będą widoczne na naszych [cennikiem](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="0aa70-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="0aa70-114">Witaj wstawki programu PowerShell w tym samouczku te informacje służą toostore tych zmiennych</span><span class="sxs-lookup"><span data-stu-id="0aa70-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="0aa70-115">Logowanie się</span><span class="sxs-lookup"><span data-stu-id="0aa70-115">Log in</span></span>

<span data-ttu-id="0aa70-116">Zaloguj się za pomocą identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0aa70-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="0aa70-117">Zaloguj się za pomocą nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0aa70-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="0aa70-118">Witaj `Login-AzureRmAccount` polecenia cmdlet zawsze wyświetla monit o podanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0aa70-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="0aa70-119">Można uniknąć monitowania za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="0aa70-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="0aa70-120">Zarządzanie kontami</span><span class="sxs-lookup"><span data-stu-id="0aa70-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="0aa70-121">Tworzenie konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0aa70-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="0aa70-122">Jeśli nie masz jeszcze [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, utwórz je.</span><span class="sxs-lookup"><span data-stu-id="0aa70-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="0aa70-123">Każde konto usługi Data Lake Analytics wymaga domyślnego konta usługi Data Lake Store używanego do przechowywania dzienników.</span><span class="sxs-lookup"><span data-stu-id="0aa70-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="0aa70-124">Można ponownie użyć istniejącego konta lub utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="0aa70-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="0aa70-125">Gdy grupa zasobów i konto magazynu usługi Data Lake Store będą dostępne, utwórz konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="0aa70-126">Uzyskiwanie informacji o koncie</span><span class="sxs-lookup"><span data-stu-id="0aa70-126">Get information about an account</span></span>

<span data-ttu-id="0aa70-127">Uzyskiwanie szczegółowych informacji o koncie.</span><span class="sxs-lookup"><span data-stu-id="0aa70-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="0aa70-128">Sprawdź hello istnienie określonego konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="0aa70-129">polecenie cmdlet Hello zwraca albo `True` lub `False`.</span><span class="sxs-lookup"><span data-stu-id="0aa70-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="0aa70-130">Sprawdź hello istnienie określonego konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0aa70-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="0aa70-131">polecenie cmdlet Hello zwraca albo `True` lub `False`.</span><span class="sxs-lookup"><span data-stu-id="0aa70-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="0aa70-132">Wyświetlanie listy kont</span><span class="sxs-lookup"><span data-stu-id="0aa70-132">Listing accounts</span></span>

<span data-ttu-id="0aa70-133">Lista Data Lake Analytics kont w obrębie hello bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0aa70-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="0aa70-134">Lista Data Lake Analytics kont w ramach określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="0aa70-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="0aa70-135">Zarządzanie regułami zapory</span><span class="sxs-lookup"><span data-stu-id="0aa70-135">Managing firewall rules</span></span>

<span data-ttu-id="0aa70-136">Lista reguł zapory.</span><span class="sxs-lookup"><span data-stu-id="0aa70-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="0aa70-137">Dodaj regułę zapory.</span><span class="sxs-lookup"><span data-stu-id="0aa70-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="0aa70-138">Zmień reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="0aa70-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="0aa70-139">Usuń regułę zapory.</span><span class="sxs-lookup"><span data-stu-id="0aa70-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="0aa70-140">Zezwalaj na adresy IP platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0aa70-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="0aa70-141">Zarządzanie źródłami danych</span><span class="sxs-lookup"><span data-stu-id="0aa70-141">Managing data sources</span></span>
<span data-ttu-id="0aa70-142">Azure Data Lake Analytics obsługuje obecnie hello następujące źródła danych:</span><span class="sxs-lookup"><span data-stu-id="0aa70-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="0aa70-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0aa70-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="0aa70-144">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0aa70-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="0aa70-145">Podczas tworzenia konta usługi Analytics należy wyznaczyć usługi Data Lake Store konta toobe hello domyślne źródło danych.</span><span class="sxs-lookup"><span data-stu-id="0aa70-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="0aa70-146">Witaj domyślnego konta usługi Data Lake Store służy toostore zadania metadanych i zadania dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="0aa70-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="0aa70-147">Po utworzeniu konta usługi Data Lake Analytics można dodać dodatkowe konta usługi Data Lake Store i/lub konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0aa70-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="0aa70-148">Znajdź hello domyślnego konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0aa70-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="0aa70-149">Można znaleźć hello domyślnego konta usługi Data Lake Store za pomocą filtrowania hello lista źródeł danych chronionych przez hello `IsDefault` właściwości:</span><span class="sxs-lookup"><span data-stu-id="0aa70-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="0aa70-150">Dodawanie źródła danych</span><span class="sxs-lookup"><span data-stu-id="0aa70-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="0aa70-151">Lista źródeł danych</span><span class="sxs-lookup"><span data-stu-id="0aa70-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="0aa70-152">Przesyłanie zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="0aa70-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="0aa70-153">Przedstawia ciąg jako skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="0aa70-153">Submit a string as a U-SQL script</span></span>

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


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="0aa70-154">Przesyłanie pliku jako skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="0aa70-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="0aa70-155">Lista zadania konta</span><span class="sxs-lookup"><span data-stu-id="0aa70-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="0aa70-156">Listę wszystkich zadań hello w hello konta.</span><span class="sxs-lookup"><span data-stu-id="0aa70-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="0aa70-157">dane wyjściowe Hello zawierają hello aktualnie uruchomione zadania i zadania, które zostały ostatnio wykonane.</span><span class="sxs-lookup"><span data-stu-id="0aa70-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="0aa70-158">Lista określoną liczbę zadań</span><span class="sxs-lookup"><span data-stu-id="0aa70-158">List a specific number of jobs</span></span>

<span data-ttu-id="0aa70-159">Domyślnie jest sortowana hello listy zadań na czas przesyłania.</span><span class="sxs-lookup"><span data-stu-id="0aa70-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="0aa70-160">Dlatego hello ostatnio przesłane zadania występować jako pierwszy.</span><span class="sxs-lookup"><span data-stu-id="0aa70-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="0aa70-161">Domyślnie program hello konta ADLA pamięta zadania na okres 180 dni, ale polecenia cmdlet hello Ge AdlJob przez domyślny zwraca hello tylko 500 pierwszych.</span><span class="sxs-lookup"><span data-stu-id="0aa70-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="0aa70-162">Użyj - Top parametru toolist określoną liczbę zadań.</span><span class="sxs-lookup"><span data-stu-id="0aa70-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="0aa70-163">Lista zadań na podstawie wartości hello właściwości zadania</span><span class="sxs-lookup"><span data-stu-id="0aa70-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="0aa70-164">Przy użyciu hello `-State` parametru.</span><span class="sxs-lookup"><span data-stu-id="0aa70-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="0aa70-165">Możesz połączyć ze sobą następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="0aa70-165">You can combine any of these values:</span></span>

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

<span data-ttu-id="0aa70-166">Użyj hello `-Result` toodetect parametru czy zakończonych zadań została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0aa70-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="0aa70-167">Ma ona następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="0aa70-167">It has these values:</span></span>

* <span data-ttu-id="0aa70-168">Anulowane</span><span class="sxs-lookup"><span data-stu-id="0aa70-168">Cancelled</span></span>
* <span data-ttu-id="0aa70-169">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0aa70-169">Failed</span></span>
* <span data-ttu-id="0aa70-170">Brak</span><span class="sxs-lookup"><span data-stu-id="0aa70-170">None</span></span>
* <span data-ttu-id="0aa70-171">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="0aa70-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="0aa70-172">Witaj `-Submitter` parametru pomagają określić, kto przesłać zadania.</span><span class="sxs-lookup"><span data-stu-id="0aa70-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="0aa70-173">Witaj `-SubmittedAfter` jest przydatny do filtrowania tooa zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="0aa70-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="0aa70-174">Typowe scenariusze dotyczące wyświetlania zadań</span><span class="sxs-lookup"><span data-stu-id="0aa70-174">Common scenarios for listing jobs</span></span>


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

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="0aa70-175">Filtrowanie listy zadań</span><span class="sxs-lookup"><span data-stu-id="0aa70-175">Filtering a list of jobs</span></span>

<span data-ttu-id="0aa70-176">Po utworzeniu listy zadań w bieżącej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aa70-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="0aa70-177">Można użyć normalnej listy hello toofilter poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aa70-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="0aa70-178">Filtr listy zadań toohello zadania przesłane w hello ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="0aa70-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="0aa70-179">Filtrowanie listy zadań toohello zadania, które zostało zakończone w hello w ostatnich 24 godzinach</span><span class="sxs-lookup"><span data-stu-id="0aa70-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="0aa70-180">Filtrowanie listy zadań toohello zadania, które uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="0aa70-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="0aa70-181">Zadania może się nie powieść w czasie kompilacji - i dlatego nigdy nie uruchamia.</span><span class="sxs-lookup"><span data-stu-id="0aa70-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="0aa70-182">Przyjrzyjmy się zadania hello nie powiodło się, które faktycznie uruchomienia, a następnie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0aa70-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="0aa70-183">Analizowanie listy zadań</span><span class="sxs-lookup"><span data-stu-id="0aa70-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="0aa70-184">Użyj hello `Group-Object` tooanalyze polecenia cmdlet listy zadań.</span><span class="sxs-lookup"><span data-stu-id="0aa70-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

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
<span data-ttu-id="0aa70-185">Podczas przeprowadzania analizy, może to być przydatne tooadd właściwości toohello zadania obiektów toomake filtrowania i grupowania prostsze.</span><span class="sxs-lookup"><span data-stu-id="0aa70-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="0aa70-186">powitania po fragment kodu przedstawia obliczania tooannotate a informacji o zadaniu z właściwości.</span><span class="sxs-lookup"><span data-stu-id="0aa70-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="0aa70-187">Pobieranie informacji o potoki i powtórzeń</span><span class="sxs-lookup"><span data-stu-id="0aa70-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="0aa70-188">Użyj hello `Get-AdlJobPipeline` polecenia cmdlet toosee hello potoku informacji wcześniej zgłoszonych zadania.</span><span class="sxs-lookup"><span data-stu-id="0aa70-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="0aa70-189">Użyj hello `Get-AdlJobRecurrence` informacje o cyklu hello toosee polecenia cmdlet dla poprzednio przesłany zadań.</span><span class="sxs-lookup"><span data-stu-id="0aa70-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="0aa70-190">Pobierz informacje o zadaniu</span><span class="sxs-lookup"><span data-stu-id="0aa70-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="0aa70-191">Pobierz stan zadania</span><span class="sxs-lookup"><span data-stu-id="0aa70-191">Get job status</span></span>

<span data-ttu-id="0aa70-192">Pobierz stan hello danego zadania.</span><span class="sxs-lookup"><span data-stu-id="0aa70-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="0aa70-193">Sprawdź dane wyjściowe zadania hello</span><span class="sxs-lookup"><span data-stu-id="0aa70-193">Examine hello job outputs</span></span>

<span data-ttu-id="0aa70-194">Po zakończeniu zadania hello, sprawdź, czy plik wyjściowy hello istnieje poprzez wyszczególnienie hello pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="0aa70-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="0aa70-195">Zarządzanie uruchomionych zadań</span><span class="sxs-lookup"><span data-stu-id="0aa70-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="0aa70-196">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="0aa70-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="0aa70-197">Poczekaj, aż toofinish zadania</span><span class="sxs-lookup"><span data-stu-id="0aa70-197">Wait for a job toofinish</span></span>

<span data-ttu-id="0aa70-198">Zamiast powtarzające się `Get-AdlAnalyticsJob` zakończenie zadania można użyć hello `Wait-AdlJob` toowait polecenia cmdlet dla hello tooend zadania.</span><span class="sxs-lookup"><span data-stu-id="0aa70-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="0aa70-199">Zarządzanie zasadami obliczeń</span><span class="sxs-lookup"><span data-stu-id="0aa70-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="0aa70-200">Wyświetl listę istniejących zasad obliczeń</span><span class="sxs-lookup"><span data-stu-id="0aa70-200">List existing compute policies</span></span>

<span data-ttu-id="0aa70-201">Witaj `Get-AdlAnalyticsComputePolicy` polecenie cmdlet pobiera informacje o zasadach obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="0aa70-202">Tworzenie zasad obliczeń</span><span class="sxs-lookup"><span data-stu-id="0aa70-202">Create a compute policy</span></span>

<span data-ttu-id="0aa70-203">Witaj `New-AdlAnalyticsComputePolicy` polecenie cmdlet tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0aa70-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="0aa70-204">W przykładzie zestawy hello maksymalna toohello dostępne AUs określony too50 użytkownika i too250 priorytet zadania minimalna hello.</span><span class="sxs-lookup"><span data-stu-id="0aa70-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="0aa70-205">Sprawdź, czy istnieje plik hello.</span><span class="sxs-lookup"><span data-stu-id="0aa70-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="0aa70-206">Przekazywanie i pobieranie</span><span class="sxs-lookup"><span data-stu-id="0aa70-206">Uploading and downloading</span></span>

<span data-ttu-id="0aa70-207">Przekaż plik.</span><span class="sxs-lookup"><span data-stu-id="0aa70-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="0aa70-208">Przekaż rekursywnie całego folderu.</span><span class="sxs-lookup"><span data-stu-id="0aa70-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="0aa70-209">Pobierz plik.</span><span class="sxs-lookup"><span data-stu-id="0aa70-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="0aa70-210">Pobierz rekursywnie całego folderu.</span><span class="sxs-lookup"><span data-stu-id="0aa70-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="0aa70-211">Jeśli hello przekazać lub proces pobierania zostanie przerwany, możesz spróbować tooresume hello procesu uruchomionego cmdlet hello ponownie z hello ``-Resume`` flagi.</span><span class="sxs-lookup"><span data-stu-id="0aa70-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="0aa70-212">Zarządzanie elementów katalogu</span><span class="sxs-lookup"><span data-stu-id="0aa70-212">Manage catalog items</span></span>

<span data-ttu-id="0aa70-213">wykaz Hello U-SQL jest toostructure używanych danych i kod, aby mogły być udostępniane przez skrypty U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0aa70-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="0aa70-214">wykaz Hello umożliwia hello najwyższym możliwym poziomie wydajności z danymi w usłudze Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0aa70-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="0aa70-215">Więcej informacji znajduje się w temacie [Używanie katalogu U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="0aa70-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="0aa70-216">Elementy listy w katalogu hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="0aa70-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="0aa70-217">Wyświetl listę wszystkich zestawów hello w wszystkich hello baz danych na koncie ADLA.</span><span class="sxs-lookup"><span data-stu-id="0aa70-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="0aa70-218">Uzyskiwanie szczegółowych informacji o elemencie katalogu</span><span class="sxs-lookup"><span data-stu-id="0aa70-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="0aa70-219">Utwórz poświadczenia w katalogu</span><span class="sxs-lookup"><span data-stu-id="0aa70-219">Create credentials in a catalog</span></span>

<span data-ttu-id="0aa70-220">W bazie danych U-SQL Utwórz obiekt poświadczeń dla bazy danych hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0aa70-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="0aa70-221">Obecnie U-SQL poświadczenia są jedynym typem hello elementu katalogu, który można utworzyć za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aa70-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="0aa70-222">Uzyskać podstawowe informacje o koncie ADLA</span><span class="sxs-lookup"><span data-stu-id="0aa70-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="0aa70-223">Wyszukuje określoną nazwę konta, podstawowe informacje o koncie hello hello następującego kodu</span><span class="sxs-lookup"><span data-stu-id="0aa70-223">Given an account name, hello following code looks up basic information about hello account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="0aa70-224">Praca z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0aa70-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="0aa70-225">Uzyskiwanie szczegółowych informacji o błędach AzureRm</span><span class="sxs-lookup"><span data-stu-id="0aa70-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="0aa70-226">Sprawdź, czy są uruchomione jako administrator</span><span class="sxs-lookup"><span data-stu-id="0aa70-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="0aa70-227">Znajdowanie identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="0aa70-227">Find a TenantID</span></span>

<span data-ttu-id="0aa70-228">Na podstawie nazwy subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="0aa70-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="0aa70-229">Z identyfikatorem subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="0aa70-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="0aa70-230">Z adresu domeny, takie jak "contoso.com"</span><span class="sxs-lookup"><span data-stu-id="0aa70-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="0aa70-231">Wyświetl listę wszystkich subskrypcji i dzierżawców identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="0aa70-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="0aa70-232">Utwórz konto usługi Data Lake Analytics przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="0aa70-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="0aa70-233">Można także użyć szablonu grupy zasobów platformy Azure przy użyciu hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0aa70-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

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

<span data-ttu-id="0aa70-234">Aby uzyskać więcej informacji, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) i [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0aa70-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0aa70-235">**Przykład szablonu**</span><span class="sxs-lookup"><span data-stu-id="0aa70-235">**Example template**</span></span>

<span data-ttu-id="0aa70-236">Zapisz hello następującego tekstu jako tekstu zawierającego `.json` pliku, a następnie użyj hello poprzedzających szablonu hello toouse skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0aa70-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="0aa70-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0aa70-237">Next steps</span></span>
* [<span data-ttu-id="0aa70-238">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0aa70-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="0aa70-239">Wprowadzenie do usługi Data Lake Analytics przy użyciu [portalu Azure](data-lake-analytics-get-started-portal.md) | [programu Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [2.0 interfejsu wiersza polecenia](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="0aa70-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="0aa70-240">Zarządzanie usługą Azure Data Lake Analytics przy użyciu [portalu Azure](data-lake-analytics-manage-use-portal.md) | [programu Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [interfejsu wiersza polecenia](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0aa70-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
