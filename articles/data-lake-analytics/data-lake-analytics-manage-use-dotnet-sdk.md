---
title: "aaaManage przy użyciu zestawu Azure .NET SDK usługi Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage usługi Data Lake Analytics zadania, źródła danych użytkowników. "
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
ms.openlocfilehash: 98630ba411823644a8bce1f1b0c1331f689cbb0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-net-sdk"></a><span data-ttu-id="d1b5e-103">Zarządzanie przy użyciu zestawu Azure .NET SDK usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d1b5e-103">Manage Azure Data Lake Analytics using Azure .NET SDK</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="d1b5e-104">Dowiedz się, jak toomanage kont usługi Azure Data Lake Analytics, źródeł danych użytkowników i zadań za pomocą hello Azure .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure .NET SDK.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d1b5e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1b5e-105">Prerequisites</span></span>

* <span data-ttu-id="d1b5e-106">**Zainstalowany program Visual Studio 2015, Visual Studio 2013 Update 4 lub Visual Studio 2012 z językiem Visual C++**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-106">**Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed**.</span></span>
* <span data-ttu-id="d1b5e-107">**Zestaw Microsoft Azure SDK dla programu .NET w wersji 2.5 lub nowszej**.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-107">**Microsoft Azure SDK for .NET version 2.5 or above**.</span></span>  <span data-ttu-id="d1b5e-108">Zainstalować go za pomocą hello [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-108">Install it using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="d1b5e-109">**Pakiety NuGet wymagane**</span><span class="sxs-lookup"><span data-stu-id="d1b5e-109">**Required NuGet Packages**</span></span>

### <a name="install-nuget-packages"></a><span data-ttu-id="d1b5e-110">Instalowanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="d1b5e-110">Install NuGet packages</span></span>

|<span data-ttu-id="d1b5e-111">Pakiet</span><span class="sxs-lookup"><span data-stu-id="d1b5e-111">Package</span></span>|<span data-ttu-id="d1b5e-112">Wersja</span><span class="sxs-lookup"><span data-stu-id="d1b5e-112">Version</span></span>|
|-------|-------|
|[<span data-ttu-id="d1b5e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span><span class="sxs-lookup"><span data-stu-id="d1b5e-113">Microsoft.Rest.ClientRuntime.Azure.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.Rest.ClientRuntime.Azure.Authentication)| <span data-ttu-id="d1b5e-114">2.3.1</span><span class="sxs-lookup"><span data-stu-id="d1b5e-114">2.3.1</span></span>|
|[<span data-ttu-id="d1b5e-115">Microsoft.Azure.Management.DataLake.Analytics</span><span class="sxs-lookup"><span data-stu-id="d1b5e-115">Microsoft.Azure.Management.DataLake.Analytics</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)|<span data-ttu-id="d1b5e-116">3.0.0</span><span class="sxs-lookup"><span data-stu-id="d1b5e-116">3.0.0</span></span>|
|[<span data-ttu-id="d1b5e-117">Microsoft.Azure.Management.DataLake.Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-117">Microsoft.Azure.Management.DataLake.Store</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)|<span data-ttu-id="d1b5e-118">2.2.0</span><span class="sxs-lookup"><span data-stu-id="d1b5e-118">2.2.0</span></span>|
|[<span data-ttu-id="d1b5e-119">Microsoft.Azure.Management.ResourceManager</span><span class="sxs-lookup"><span data-stu-id="d1b5e-119">Microsoft.Azure.Management.ResourceManager</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="d1b5e-120">1.6.0-Preview</span><span class="sxs-lookup"><span data-stu-id="d1b5e-120">1.6.0-preview</span></span>|
|[<span data-ttu-id="d1b5e-121">Microsoft.Azure.Graph.RBAC</span><span class="sxs-lookup"><span data-stu-id="d1b5e-121">Microsoft.Azure.Graph.RBAC</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager)|<span data-ttu-id="d1b5e-122">3.4.0-Preview</span><span class="sxs-lookup"><span data-stu-id="d1b5e-122">3.4.0-preview</span></span>|

<span data-ttu-id="d1b5e-123">Można zainstalować te pakiety przy użyciu wiersza polecenia NuGet hello z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-123">You can install these packages via hello NuGet command line with hello following commands:</span></span>

```
Install-Package -Id Microsoft.Rest.ClientRuntime.Azure.Authentication  -Version 2.3.1
Install-Package -Id Microsoft.Azure.Management.DataLake.Analytics  -Version 3.0.0
Install-Package -Id Microsoft.Azure.Management.DataLake.Store  -Version 2.2.0
Install-Package -Id Microsoft.Azure.Management.ResourceManager  -Version 1.6.0-preview
Install-Package -Id Microsoft.Azure.Graph.RBAC -Version 3.4.0-preview
```

## <a name="common-variables"></a><span data-ttu-id="d1b5e-124">Zmienne typowych</span><span class="sxs-lookup"><span data-stu-id="d1b5e-124">Common variables</span></span>

``` csharp
string subid = "<Subscription ID>"; // Subscription ID (a GUID)
string tenantid = "<Tenant ID>"; // AAD tenant ID or domain. For example, "contoso.onmicrosoft.com"
string rg == "<value>"; // Resource  group name
string clientid = "1950a258-227b-4e31-a9cf-717495945fc2"; // Sample client ID (this will work, but you should pick your own)
```

## <a name="authentication"></a><span data-ttu-id="d1b5e-125">Authentication</span><span class="sxs-lookup"><span data-stu-id="d1b5e-125">Authentication</span></span>

<span data-ttu-id="d1b5e-126">Istnieje wiele opcji logowania tooAzure usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-126">You have multiple options for logging on tooAzure Data Lake Analytics.</span></span> <span data-ttu-id="d1b5e-127">Witaj następujący fragment kodu przedstawiono przykład uwierzytelnianie za pomocą interakcyjnego uwierzytelniania użytkownika z okno podręczne.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-127">hello following snippet shows an example of authentication with interactive user authentication with a pop-up.</span></span>

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

<span data-ttu-id="d1b5e-128">Witaj kod źródłowy **GetCreds_User_Popup** i hello kodu dla inne opcje uwierzytelniania są objęte [opcje uwierzytelniania Data Lake Analytics .NET](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span><span class="sxs-lookup"><span data-stu-id="d1b5e-128">hello source code for **GetCreds_User_Popup** and hello code for other options for authentication are covered in [Data Lake Analytics .NET authentication options](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options)</span></span>


## <a name="create-hello-client-management-objects"></a><span data-ttu-id="d1b5e-129">Tworzenie obiektów zarządzania powitania klienta</span><span class="sxs-lookup"><span data-stu-id="d1b5e-129">Create hello client management objects</span></span>

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

## <a name="manage-accounts"></a><span data-ttu-id="d1b5e-130">Zarządzanie kontami</span><span class="sxs-lookup"><span data-stu-id="d1b5e-130">Manage accounts</span></span>

### <a name="create-an-azure-resource-group"></a><span data-ttu-id="d1b5e-131">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1b5e-131">Create an Azure Resource Group</span></span>

<span data-ttu-id="d1b5e-132">Jeśli jeszcze nie utworzono jedną, musi mieć toocreate grupy zasobów platformy Azure składniki usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-132">If you haven't already created one, you must have an Azure Resource Group toocreate your Data Lake Analytics components.</span></span> <span data-ttu-id="d1b5e-133">Wymagane poświadczenia uwierzytelniania, identyfikator subskrypcji i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-133">You  need your authentication credentials, subscription ID, and a location.</span></span> <span data-ttu-id="d1b5e-134">Witaj następującego kodu pokazuje sposób toocreate grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-134">hello following code shows how toocreate a resource group:</span></span>

``` csharp
var resourceGroup = new ResourceGroup { Location = location };
resourceManagementClient.ResourceGroups.CreateOrUpdate(groupName, rg);
```
<span data-ttu-id="d1b5e-135">Aby uzyskać więcej informacji, zobacz [grup zasobów platformy Azure i usługi Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span><span class="sxs-lookup"><span data-stu-id="d1b5e-135">For more information, see [Azure Resource Groups and Data Lake Analytics](#Azure-Resource-Groups-and-Data-Lake-Analytics).</span></span>

### <a name="create-a-data-lake-store-account"></a><span data-ttu-id="d1b5e-136">Tworzenie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-136">Create a Data Lake Store account</span></span>

<span data-ttu-id="d1b5e-137">Kiedykolwiek ADLA konto wymaga koncie ADLS.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-137">Ever ADLA account requires an ADLS account.</span></span> <span data-ttu-id="d1b5e-138">Jeśli nie masz jeszcze jeden toouse, można utworzyć jedną z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-138">If you don't already have one toouse, you can create one with hello following code:</span></span>

``` csharp
var new_adls_params = new DataLakeStoreAccount(location: _location);
adlsAccountClient.Account.Create(rg, adls, new_adls_params);
```

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="d1b5e-139">Tworzenie konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d1b5e-139">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="d1b5e-140">Witaj następującego kodu tworzy konto ADLS</span><span class="sxs-lookup"><span data-stu-id="d1b5e-140">hello following code creates an ADLS account</span></span>

``` csharp
var new_adla_params = new DataLakeAnalyticsAccount()
{
   DefaultDataLakeStoreAccount = adls,
   Location = location
};

adlaClient.Account.Create(rg, adla, new_adla_params);
```

### <a name="list-data-lake-store-accounts"></a><span data-ttu-id="d1b5e-141">Konta usługi Data Lake Store listy</span><span class="sxs-lookup"><span data-stu-id="d1b5e-141">List Data Lake Store accounts</span></span>

``` csharp
var adlsAccounts = adlsAccountClient.Account.List().ToList();
foreach (var adls in adlsAccounts)
{
   Console.WriteLine($"ADLS: {0}", adls.Name);
}
```

### <a name="list-data-lake-analytics-accounts"></a><span data-ttu-id="d1b5e-142">Lista Data Lake Analytics kont</span><span class="sxs-lookup"><span data-stu-id="d1b5e-142">List Data Lake Analytics accounts</span></span>

``` csharp
var adlaAccounts = adlaClient.Account.List().ToList();

for (var adla in AdlaAccounts)
{
   Console.WriteLine($"ADLA: {0}, adla.Name");
}
```

### <a name="checking-if-an-account-exists"></a><span data-ttu-id="d1b5e-143">Sprawdzanie, czy konto istnieje</span><span class="sxs-lookup"><span data-stu-id="d1b5e-143">Checking if an account exists</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="d1b5e-144">Uzyskiwanie informacji o koncie</span><span class="sxs-lookup"><span data-stu-id="d1b5e-144">Get information about an account</span></span>

``` csharp
bool exists = adlaClient.Account.Exists(rg, adla));
if (exists)
{
   var adla_accnt = adlaClient.Account.Get(rg, adla);
}
```

### <a name="delete-an-account"></a><span data-ttu-id="d1b5e-145">Usuń konto</span><span class="sxs-lookup"><span data-stu-id="d1b5e-145">Delete an account</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
   adlaClient.Account.Delete(rg, adla);
}
```

### <a name="get-hello-default-data-lake-store-account"></a><span data-ttu-id="d1b5e-146">Pobierz hello domyślnego konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-146">Get hello default Data Lake Store account</span></span>

<span data-ttu-id="d1b5e-147">Każde konto usługi Data Lake Analytics wymaga domyślnego konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-147">Every Data Lake Analytics account requires a default Data Lake Store account.</span></span> <span data-ttu-id="d1b5e-148">Używają tego konta magazynu kodu toodetermine hello domyślnego konta usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-148">Use this code toodetermine hello default Store account for an Analytics account.</span></span>

``` csharp
if (adlaClient.Account.Exists(rg, adla))
{
  var adla_accnt = adlaClient.Account.Get(rg, adla);
  string def_adls_account = adla_accnt.DefaultDataLakeStoreAccount;
}
```

## <a name="manage-data-sources"></a><span data-ttu-id="d1b5e-149">Zarządzaj źródłami danych</span><span class="sxs-lookup"><span data-stu-id="d1b5e-149">Manage data sources</span></span>

<span data-ttu-id="d1b5e-150">Data Lake Analytics obsługuje obecnie hello następujące źródła danych:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-150">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="d1b5e-151">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-151">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="d1b5e-152">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d1b5e-152">Azure Storage Account</span></span>](../storage/common/storage-introduction.md)

### <a name="link-tooan-azure-storage-account"></a><span data-ttu-id="d1b5e-153">Łącze tooan konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d1b5e-153">Link tooan Azure Storage account</span></span>

<span data-ttu-id="d1b5e-154">Można tworzyć łącza tooAzure kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-154">You can create links tooAzure Storage accounts.</span></span>

``` csharp
string storage_key = "xxxxxxxxxxxxxxxxxxxx";
string storage_account = "mystorageaccount";
var addParams = new AddStorageAccountParameters(storage_key);            
adlaClient.StorageAccounts.Add(rg, adla, storage_account, addParams);
```

### <a name="list-azure-storage-data-sources"></a><span data-ttu-id="d1b5e-155">Listy źródeł danych usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d1b5e-155">List Azure Storage data sources</span></span>

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

### <a name="list-data-lake-store-data-sources"></a><span data-ttu-id="d1b5e-156">Źródła danych listy Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-156">List Data Lake Store data sources</span></span>

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

### <a name="upload-and-download-folders-and-files"></a><span data-ttu-id="d1b5e-157">Przekazywanie i pobieranie plików i folderów</span><span class="sxs-lookup"><span data-stu-id="d1b5e-157">Upload and download folders and files</span></span>
<span data-ttu-id="d1b5e-158">Można użyć hello Data Lake — magazyn plików systemu klienta zarządzania obiektu tooupload i Pobierz pojedyncze pliki lub foldery z komputera lokalnego Azure tooyour, przy użyciu następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-158">You can use hello Data Lake Store file system client management object tooupload and download individual files or folders from Azure tooyour local computer, using hello following methods:</span></span>

- <span data-ttu-id="d1b5e-159">UploadFolder</span><span class="sxs-lookup"><span data-stu-id="d1b5e-159">UploadFolder</span></span>
- <span data-ttu-id="d1b5e-160">UploadFile</span><span class="sxs-lookup"><span data-stu-id="d1b5e-160">UploadFile</span></span>
- <span data-ttu-id="d1b5e-161">DownloadFolder</span><span class="sxs-lookup"><span data-stu-id="d1b5e-161">DownloadFolder</span></span>
- <span data-ttu-id="d1b5e-162">DownloadFile</span><span class="sxs-lookup"><span data-stu-id="d1b5e-162">DownloadFile</span></span>

<span data-ttu-id="d1b5e-163">pierwszy parametr Hello dotyczącej tych metod jest nazwa hello hello konta usługi Data Lake magazynu, następuje parametrów hello ścieżka źródłowa i ścieżka docelowa hello.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-163">hello first parameter for these methods is hello name of hello Data Lake Store Account, followed by parameters for hello source path and hello destination path.</span></span>

<span data-ttu-id="d1b5e-164">Witaj poniższy przykład pokazuje, jak toodownload folder w hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-164">hello following example shows how toodownload a folder in hello Data Lake Store.</span></span>

``` csharp
adlsFileSystemClient.FileSystem.DownloadFolder(adls, sourcePath, destinationPath);
```

### <a name="create-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="d1b5e-165">Utwórz plik w ramach konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d1b5e-165">Create a file in a Data Lake Store account</span></span>

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

### <a name="verify-azure-storage-account-paths"></a><span data-ttu-id="d1b5e-166">Sprawdź ścieżek konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="d1b5e-166">Verify Azure Storage account paths</span></span>
<span data-ttu-id="d1b5e-167">Witaj następujący kod sprawdza konto magazynu Azure (storageAccntName) istnieje w ramach konta usługi Data Lake Analytics (analyticsAccountName), a kontener (containerName) istnieje na koncie magazynu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-167">hello following code checks if an Azure Storage account (storageAccntName) exists in a Data Lake Analytics account (analyticsAccountName), and if a container (containerName) exists in hello Azure Storage account.</span></span>

``` csharp
string storage_account = "mystorageaccount";
string storage_container = "mycontainer";
bool accountExists = adlaClient.Account.StorageAccountExists(rg, adla, storage_account));
bool containerExists = adlaClient.Account.StorageContainerExists(rg, adla, storage_account, storage_container));
```

## <a name="manage-catalog-and-jobs"></a><span data-ttu-id="d1b5e-168">Zarządzanie katalogu i zadań</span><span class="sxs-lookup"><span data-stu-id="d1b5e-168">Manage catalog and jobs</span></span>
<span data-ttu-id="d1b5e-169">Obiekt DataLakeAnalyticsCatalogManagementClient Hello zapewnia metody do zarządzania bazą danych SQL hello podane dla każdego konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-169">hello DataLakeAnalyticsCatalogManagementClient object provides methods for managing hello SQL database provided for each Azure Data Lake Analytics account.</span></span> <span data-ttu-id="d1b5e-170">Witaj DataLakeAnalyticsJobManagementClient udostępnia metody toosubmit i zarządzaj nimi zadania są uruchamiane w bazie danych hello ze skryptów U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-170">hello DataLakeAnalyticsJobManagementClient provides methods toosubmit and manage jobs run on hello database with U-SQL scripts.</span></span>

### <a name="list-databases-and-schemas"></a><span data-ttu-id="d1b5e-171">Lista baz danych i schematy</span><span class="sxs-lookup"><span data-stu-id="d1b5e-171">List databases and schemas</span></span>
<span data-ttu-id="d1b5e-172">Wśród hello kilka czynników, które można wyświetlić w najbardziej typowych hello są baz danych i ich schematu.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-172">Among hello several things you can list, hello most common are databases and their schema.</span></span> <span data-ttu-id="d1b5e-173">Witaj następujący kod uzyskuje kolekcji baz danych, a następnie wylicza hello schematu dla każdej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-173">hello following code obtains a collection of databases, and then enumerates hello schema for each database.</span></span>

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

### <a name="list-table-columns"></a><span data-ttu-id="d1b5e-174">Lista kolumn tabeli</span><span class="sxs-lookup"><span data-stu-id="d1b5e-174">List table columns</span></span>
<span data-ttu-id="d1b5e-175">Witaj poniższy kod przedstawia sposób tooaccess hello bazy danych z katalogu Data Lake Analytics zarządzania klienta toolist hello kolumn w określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-175">hello following code shows how tooaccess hello database with a Data Lake Analytics Catalog management client toolist hello columns in a specified table.</span></span>

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

### <a name="list-failed-jobs"></a><span data-ttu-id="d1b5e-176">Lista zadań zakończonych niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="d1b5e-176">List failed jobs</span></span>
<span data-ttu-id="d1b5e-177">Hello następujący kod wyświetla informacje o zadaniach, których nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-177">hello following code lists information about jobs that failed.</span></span>

``` csharp
var odq = new ODataQuery<JobInformation> { Filter = "result eq 'Failed'" };
var jobs = adlaJobClient.Job.List(adla, odq);
foreach (var j in jobs)
{
   Console.WriteLine($"{j.Name}\t{j.JobId}\t{j.Type}\t{j.StartTime}\t{j.EndTime}");
}
```

### <a name="list-pipelines"></a><span data-ttu-id="d1b5e-178">Potoki listy</span><span class="sxs-lookup"><span data-stu-id="d1b5e-178">List pipelines</span></span>
<span data-ttu-id="d1b5e-179">Hello poniższy kod wyświetla informacje o poszczególnych potoku zadania konta toohello zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-179">hello following code lists information about each pipeline of jobs submitted toohello account.</span></span>

``` csharp
var pipelines = adlaJobClient.Pipeline.List(adla);
foreach (var p in pipelines)
{
   Console.WriteLine($"Pipeline: {p.Name}\t{p.PipelineId}\t{p.LastSubmitTime}");
}
```

### <a name="list-recurrences"></a><span data-ttu-id="d1b5e-180">Cykle listy</span><span class="sxs-lookup"><span data-stu-id="d1b5e-180">List recurrences</span></span>
<span data-ttu-id="d1b5e-181">Hello poniższy kod wyświetla informacje o każdym cyklu zadania konta toohello zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-181">hello following code lists information about each recurrence of jobs submitted toohello account.</span></span>

``` csharp
var recurrences = adlaJobClient.Recurrence.List(adla);
foreach (var r in recurrences)
{
   Console.WriteLine($"Recurrence: {r.Name}\t{r.RecurrenceId}\t{r.LastSubmitTime}");
}
```

## <a name="common-graph-scenarios"></a><span data-ttu-id="d1b5e-182">Typowe scenariusze wykresu</span><span class="sxs-lookup"><span data-stu-id="d1b5e-182">Common graph scenarios</span></span>

### <a name="look-up-user-in-hello-aad-directory"></a><span data-ttu-id="d1b5e-183">Wyszukiwanie użytkowników w katalogu usługi AAD hello</span><span class="sxs-lookup"><span data-stu-id="d1b5e-183">Look up user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
```

### <a name="get-hello-objectid-of-a-user-in-hello-aad-directory"></a><span data-ttu-id="d1b5e-184">Pobierz hello ObjectId użytkownika w katalogu usługi AAD hello</span><span class="sxs-lookup"><span data-stu-id="d1b5e-184">Get hello ObjectId of a user in hello AAD directory</span></span>

``` csharp
var userinfo = graphClient.Users.Get( "bill@contoso.com" );
Console.WriteLine( userinfo.ObjectId )
```

## <a name="manage-compute-policies"></a><span data-ttu-id="d1b5e-185">Zarządzanie zasadami obliczeń</span><span class="sxs-lookup"><span data-stu-id="d1b5e-185">Manage compute policies</span></span>
<span data-ttu-id="d1b5e-186">Obiekt DataLakeAnalyticsAccountManagementClient Hello zapewnia metody do zarządzania hello obliczeniowe zasady dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-186">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="d1b5e-187">Podać zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="d1b5e-187">List compute policies</span></span>
<span data-ttu-id="d1b5e-188">powitania po kod pobiera listę zasad obliczeniowe dla konta usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-188">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

``` csharp
var policies = adlaAccountClient.ComputePolicies.ListByAccount(rg, adla);
foreach (var p in policies)
{
   Console.WriteLine($"Name: {p.Name}\tType: {p.ObjectType}\tMax AUs / job: {p.MaxDegreeOfParallelismPerJob}\tMin priority / job: {p.MinPriorityPerJob}");
}
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="d1b5e-189">Utwórz nowe zasady obliczeń</span><span class="sxs-lookup"><span data-stu-id="d1b5e-189">Create a new compute policy</span></span>
<span data-ttu-id="d1b5e-190">powitania po kod tworzy nową zasadę obliczeniowe dla konta usługi Data Lake Analytics, ustawienie hello maksymalną AUs dostępne toohello określonego użytkownika too50 i too250 priorytet zadania minimalna hello.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-190">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

``` csharp
var userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde";
var newPolicyParams = new ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250);
adlaAccountClient.ComputePolicies.CreateOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams);
```

## <a name="next-steps"></a><span data-ttu-id="d1b5e-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1b5e-191">Next steps</span></span>
* [<span data-ttu-id="d1b5e-192">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d1b5e-192">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d1b5e-193">Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1b5e-193">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="d1b5e-194">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1b5e-194">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
