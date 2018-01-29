---
title: "Zarządzanie przy użyciu zestawu Azure .NET SDK usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać zadań usługi Data Lake Analytics, źródła danych i użytkowników. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 811d172d-9873-4ce9-a6d5-c1a26b374c79
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 0f8a95f96ce4c816dfb9132923faa9a9bf20c205
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a>Zarządzanie przy użyciu zestawu Azure .NET SDK usługi Azure Data Lake Analytics
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Dowiedz się, jak zarządzać kontami usługi Azure Data Lake Analytics, źródła danych, użytkowników i zadań przy użyciu zestawu .NET SDK usługi Azure. 

## <a name="prerequisites"></a>Wymagania wstępne

* **Zainstalowany program Visual Studio 2015, Visual Studio 2013 Update 4 lub Visual Studio 2012 z językiem Visual C++**.
* **Zestaw Microsoft Azure SDK dla programu .NET w wersji 2.5 lub nowszej**.  Można go zainstalować przy użyciu [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).
* **Pakiety NuGet wymagane**

### <a name="install-nuget-packages"></a>Instalowanie pakietów NuGet

|Pakiet|Wersja|
|-------|-------|
|[Microsoft.Rest.ClientRuntime.Azure.Authentication](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| 2.3.1|
|[Microsoft.Azure.Management.DataLake.Analytics](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|3.0.0|
|[Microsoft.Azure.Management.DataLake.Store](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|2.2.0|
|[Microsoft.Azure.Management.ResourceManager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|1.6.0-Preview|
|[Microsoft.Azure.Graph.RBAC](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|3.4.0-Preview|

Te pakiety przy użyciu wiersza polecenia NuGet można zainstalować za pomocą następujących poleceń:

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a>Zmienne typowych

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a>Authentication

Istnieje wiele opcji logowania do usługi Azure Data Lake Analytics. Poniższy fragment kodu przedstawia przykład uwierzytelniania przy użyciu uwierzytelniania użytkownika interaktywnego z okno podręczne.

``` csharp
using System;
using System.IO;
using System.Threading;
using System.Security.Cryptography.X509Certificates;

using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.DataLake.Analytics;
using Microsoft.Azure.Management.DataLake.Analytics.Models;
using Microsoft.Azure.Management.DataLake.Store;
using Microsoft.Azure.Management.DataLake.Store.Models;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Azure.Graph.RBAC;

public static Program
{
   public static string TENANT = "microsoft.onmicrosoft.com";
   public static string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
   public static System.Uri ARM_TOKEN_AUDIENCE = new System.Uri( @"https://management.core.windows.net/");
   public static System.Uri ADL_TOKEN_AUDIENCE = new System.Uri( @"https://datalake.azure.net/" );
   public static System.Uri GRAPH_TOKEN_AUDIENCE = new System.Uri( @"https://graph.windows.net/" );

   static void Main(string[] args)
   {
      string MY_DOCUMENTS= System.Environment.GetFolderPath( System.Environment.SpecialFolder.MyDocuments);
      string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");

      var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
      var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
      var graphCreds = GetCreds_User_Popup(TENANT, GRAPH_TOKEN_AUDIENCE, CLIENTID, tokenCache);
   }
}
```

Kod źródłowy **GetCreds_User_Popup** i kod innych opcje uwierzytelniania są objęte [opcje uwierzytelniania Data Lake Analytics .NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)


## <a name="create-the-client-management-objects"></a>Tworzenie klienta zarządzania obiektów

``` csharp
var resourceManagementClient = new ResourceManagementClient(armCreds) { SubscriptionId = subid };

var adlaAccountClient = new DataLakeAnalyticsAccountManagementClient(armCreds);
adlaAccountClient.SubscriptionId = subid;

var adlsAccountClient = new DataLakeStoreAccountManagementClient(armCreds);
adlsAccountClient.SubscriptionId = subid;

var adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClient(adlCreds);
var adlaJobClient = new DataLakeAnalyticsJobManagementClient(adlCreds);

var adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(adlCreds);

var  graphClient = new GraphRbacManagementClient(graphCreds);
graphClient.TenantID = domain;

```

## <a name="manage-accounts"></a>Zarządzanie kontami

### <a name="create-an-azure-resource-group"></a>Tworzenie grupy zasobów platformy Azure

Jeśli jeszcze nie utworzono jedną, muszą mieć grupy zasobów platformy Azure, aby utworzyć składniki usługi Data Lake Analytics. Wymagane poświadczenia uwierzytelniania, identyfikator subskrypcji i lokalizacji. Poniższy kod przedstawia sposób tworzenia grupy zasobów:

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
Aby uzyskać więcej informacji, zobacz [grup zasobów platformy Azure i usługi Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).

### <a name="create-a-data-lake-store-account"></a>Tworzenie konta usługi Data Lake Store

Kiedykolwiek ADLA konto wymaga koncie ADLS. Jeśli nie masz jeszcze jeden będzie używany, można utworzyć jedną z następującym kodem:

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a>Tworzenie konta Data Lake Analytics

Poniższy kod tworzy konto ADLS

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a>Konta usługi Data Lake Store listy

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a>Lista Data Lake Analytics kont

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a>Sprawdzanie, czy konto istnieje

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a>Uzyskiwanie informacji o koncie

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a>Usuń konto

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-the-default-data-lake-store-account"></a>Uzyskiwanie domyślnego konta usługi Data Lake Store

Każde konto usługi Data Lake Analytics wymaga domyślnego konta usługi Data Lake Store. Ten kod umożliwia określenie domyślnego konta magazynu dla konta usługi Analytics.

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a>Zarządzaj źródłami danych

Data Lake Analytics obsługuje obecnie następujących źródeł danych:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Konto magazynu Azure](../storage/common/storage-introduction.md)

### <a name="link-to-an-azure-storage-account"></a>Łącze do konta usługi Azure Storage

Można utworzyć łącza do konta usługi Azure Storage.

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a>Listy źródeł danych usługi Azure Storage

``` csharp
var stg_accounts = adlaAccountClient.StorageAccounts.ListByAccount(rg, adla);

if (stg_accounts != null)
{
  foreach (var stg_account in stg_accounts)
  {
      Console.WriteLine($"Storage account: {0}", stg_account.Name);
  }
}
```

### <a name="list-data-lake-store-data-sources"></a>Źródła danych listy Data Lake Store

``` csharp
var adls_accounts = adlsClient.Account.List();

if (adls_accounts != null)
{
  foreach (var adls_accnt in adls_accounts)
  {
      Console.WriteLine($"ADLS account: {0}", adls_accnt.Name);
  }
}
```

### <a name="upload-and-download-folders-and-files"></a>Przekazywanie i pobieranie plików i folderów
Obiektu zarządzania klient systemu plików usługi Data Lake Store służy do przekazywania i pobierania poszczególnych plików lub folderów z platformy Azure na komputerze lokalnym przy użyciu następujących metod:

- UploadFolder
- UploadFile
- DownloadFolder
- DownloadFile

Pierwszy parametr dla tych metod jest nazwa konta magazynu danych Lake, następuje parametrów ścieżka źródłowa i ścieżka docelowa.

Poniższy przykład przedstawia sposób pobierania folderu w usłudze Data Lake Store.

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a>Utwórz plik w ramach konta usługi Data Lake Store

``` csharp
using (var memstream = new MemoryStream())
{
   using (var sw = new StreamWriter(memstream, UTF8Encoding.UTF8))
   {
      sw.WriteLine("Hello World");
      sw.Flush();

      adlsFileSystemClient.FileSystem.Create(adls, "/Samples/Output/randombytes.csv", memstream);
   }
}
```

### <a name="verify-azure-storage-account-paths"></a>Sprawdź ścieżek konta magazynu Azure
Poniższy kod sprawdza konto magazynu Azure (storageAccntName) istnieje w ramach konta usługi Data Lake Analytics (analyticsAccountName), a kontener (containerName) istnieje na koncie magazynu Azure.

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a>Zarządzanie katalogu i zadań
Obiekt DataLakeAnalyticsCatalogManagementClient zapewnia metody do zarządzania bazą danych SQL podane dla każdego konta usługi Azure Data Lake Analytics. DataLakeAnalyticsJobManagementClient zawiera metody służące do przesyłania zadania i zarządzać nimi uruchomić w bazie danych ze skryptów U-SQL.

### <a name="list-databases-and-schemas"></a>Lista baz danych i schematy
Między kilka kwestii, które można wyświetlić listę najczęściej są baz danych i ich schematu. Poniższy kod uzyskuje kolekcji baz danych, a następnie wylicza schematu dla każdej bazy danych.

``` csharp
var databases = adlaCatalogClient.Catalog.ListDatabases(adla);
foreach (var db in databases)
{
  Console.WriteLine($"Database: {db.Name}");
  Console.WriteLine(" - Schemas:");
  var schemas = adlaCatalogClient.Catalog.ListSchemas(adla, db.Name);
  foreach (var schm in schemas)
  {
      Console.WriteLine($"\t{schm.Name}");
  }
}
```

### <a name="list-table-columns"></a>Lista kolumn tabeli
Poniższy kod przedstawia sposób dostępu do bazy danych z klientem do zarządzania katalogu Data Lake Analytics, aby wyświetlić listę kolumn w określonej tabeli.

``` csharp
var tbl = adlaCatalogClient.Catalog.GetTable(adla, "master", "dbo", "MyTableName");
IEnumerable<USqlTableColumn> columns = tbl.ColumnList;

foreach (USqlTableColumn utc in columns)
{
  string scriptPath = "/Samples/Scripts/SearchResults_Wikipedia_Script.txt";
  Stream scriptStrm = adlsFileSystemClient.FileSystem.Open(_adlsAccountName, scriptPath);
  string scriptTxt = string.Empty;
  using (StreamReader sr = new StreamReader(scriptStrm))
  {
      scriptTxt = sr.ReadToEnd();
  }

  var jobName = "SR_Wikipedia";
  var jobId = Guid.NewGuid();
  var properties = new USqlJobProperties(scriptTxt);
  var parameters = new JobInformation(jobName, JobType.USql, properties, priority: 1, degreeOfParallelism: 1, jobId: jobId);
  var jobInfo = adlaJobClient.Job.Create(adla, jobId, parameters);
  Console.WriteLine($"Job {jobName} submitted.");

}
```

### <a name="list-failed-jobs"></a>Lista zadań zakończonych niepowodzeniem
Poniższy kod zawiera informacje dotyczące zadań, których nie powiodła się.

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a>Potoki listy
Poniższy kod wyświetla informacje o każdym potoku zadań przesłane do konta.

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a>Cykle listy
Poniższy kod wyświetla informacje o każdym cyklu zadania przekazane do konta.

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a>Typowe scenariusze wykresu

### <a name="look-up-user-in-the-aad-directory"></a>Wyszukiwanie użytkownika w katalogu usługi AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-the-objectid-of-a-user-in-the-aad-directory"></a>Pobierz identyfikator obiektu użytkownika w katalogu usługi AAD

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a>Zarządzanie zasadami obliczeń
Obiekt DataLakeAnalyticsAccountManagementClient zapewnia metody do zarządzania zasadami obliczeniowe dla konta usługi Data Lake Analytics.

### <a name="list-compute-policies"></a>Podać zasady obliczeń
Poniższy kod pobiera listę zasad obliczeniowe dla konta usługi Data Lake Analytics.

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a>Utwórz nowe zasady obliczeń
Poniższy kod tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics, ustawienie maksymalnej AUs, dostępne do określonego użytkownika do 50, a także priorytet zadania minimalna 250.

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md)
* [Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
