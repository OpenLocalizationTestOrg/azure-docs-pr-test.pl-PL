---
title: "aaaDevelop Azure File Storage z platformą .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dane plików toodevelop .NET aplikacji i usług, które używają toostore magazyn plików Azure."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Tworzenie oprogramowania dla usługi Azure File Storage przy użyciu platformy .NET 
> [!NOTE]
> W tym artykule przedstawiono sposób toomanage magazyn plików Azure z kodu platformy .NET. toolearn więcej informacji na temat usługi Magazyn plików Azure, zobacz hello [tooAzure wprowadzenie magazyn plików](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku przedstawiono podstawy hello przy użyciu platformy .NET toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure. W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem .NET i plików platformy Azure:

* Pobierz hello zawartość pliku
* Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików hello.
* Utwórz sygnaturę dostępu współdzielonego (SAS klucza) dla pliku, która używa zasad dostępu współdzielonego zdefiniowanych w udziale hello.
* Skopiuj plik tooanother pliku hello tego samego konta magazynu.
* Skopiuj plik obiektu blob tooa hello tego samego konta magazynu.
* Rozwiązywanie problemów przy użyciu metryk usługi Azure Storage.

> [!Note]  
> Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure hello przy użyciu standardowych klas System.IO powitania dla operacji We/Wy pliku. W tym artykule opisano, jak toowrite aplikacji, które używają hello Azure magazynu .NET SDK, który używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Tworzenie aplikacji konsoli hello i uzyskiwanie zestawu hello
W programie Visual Studio utwórz nową aplikację konsoli dla systemu Windows. Hello następujące kroki pokazują, jak toocreate aplikacji konsoli w programie Visual Studio 2017, jednak hello kroki są podobne w innych wersjach programu Visual Studio.

1. Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**
2. Wybierz kolejno pozycje **Zainstalowane** > **Szablony** > **Visual C#** > **Klasyczny pulpit systemu Windows**
3. Wybierz pozycję **Aplikacja konsoli (.NET Framework)**
4. Wprowadź nazwę aplikacji w hello **Name:** pola
5. Kliknij przycisk **OK**

Wszystkie przykłady kodu, w tym samouczku można dodać toohello `Main()` metody Aplikacja konsoli `Program.cs` pliku.

Można użyć hello biblioteki klienta magazynu Azure w dowolnego typu aplikacji .NET, w tym chmury Azure usługi lub aplikacji sieci web oraz aplikacje komputerów stacjonarnych i przenośnych. W tym przewodniku dla uproszczenia przedstawiono aplikację konsolową.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Korzystanie z pakietów hello wymagane tooinstall NuGet
Istnieją dwa pakiety tooreference toocomplete Twojego projektu musi w tym samouczku:

* [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ten pakiet zapewnia dostęp programistyczny toodata zasobów na koncie magazynu.
* [Biblioteka programu Microsoft Azure Configuration Manager dla środowiska .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): ten pakiet zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji, niezależnie od tego, gdzie została uruchomiona aplikacja.

Możesz użyć NuGet tooobtain oba pakiety. Wykonaj następujące kroki:

1. Kliknij projekt prawym przyciskiem myszy w **Eksploratorze rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**.
2. Wyszukaj w trybie online "Windowsazure.Storage", a następnie kliknij przycisk **zainstalować** tooinstall hello biblioteki klienta usługi Storage oraz jej zależności.
3. Wyszukaj w trybie online "WindowsAzure.ConfigurationManager", a następnie kliknij przycisk **zainstalować** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Zapisz plik app.config toohello poświadczeń konta magazynu
Teraz zapiszemy poświadczenia w pliku app.config projektu. Edytowanie pliku app.config hello wygląda tak, jakby toohello podobnie poniższy przykład, zastępując `myaccount` z nazwę konta magazynu i `mykey` kluczem konta magazynu.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> najnowszą wersję Hello hello emulatora magazynu Azure nie obsługuje usługi Magazyn plików Azure. Parametry połączenia muszą wskazywać konto magazynu Azure w hello toowork chmury z magazynem plików Azure.

## <a name="add-using-directives"></a>Dodawanie dyrektyw using
Otwórz hello `Program.cs` plików w Eksploratorze rozwiązań i dodaj następujące hello przy użyciu dyrektywy toohello górnej części pliku hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Udział plików hello dostępu programowo
Następnie dodaj hello następującego kodu toohello `Main()` ciąg połączenia hello tooretrieve — metoda (po kodzie hello pokazanym powyżej). Ten kod pobiera odwołanie do pliku toohello utworzonego wcześniej i wyświetla okno konsoli toohello jego zawartość.

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Uruchom dane wyjściowe hello toosee hello konsoli aplikacji.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Ustaw maksymalny rozmiar hello udziału plików
Począwszy od wersji 5.x biblioteki klienta magazynu Azure hello, można skonfigurować zestaw hello przydziału (lub maksymalny rozmiar) udziału plików w gigabajtach. Można również sprawdzić, jak dużo danych jest obecnie przechowywanych w udziale hello toosee.

Przez ustawienie hello limitu przydziału dla udziału można ograniczyć całkowity rozmiar plików hello przechowywanych w udziale hello hello. Jeśli całkowity rozmiar plików w udziale hello hello przekracza przydział hello ustawiony na powitania udziału, a następnie klienci będą tooincrease hello rozmiaru istniejących plików lub tworzenia nowych plików, chyba że te pliki są puste.

w poniższym przykładzie Hello pokazuje, jak toocheck hello bieżące użycie udziału oraz jak tooset hello przydziału udziału hello.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generowanie sygnatury dostępu współdzielonego dla pliku lub udziału plików
Począwszy od wersji 5.x hello biblioteki klienta magazynu Azure, można wygenerować sygnaturę dostępu współdzielonego (SAS) dla udziału plików lub dla pojedynczego pliku. Można również tworzyć zasady dostępu współużytkowanego na dostęp do udostępnionych toomanage udziału plików podpisy. Tworzenie zasad dostępu współdzielonego jest zalecane, ponieważ umożliwia cofnięcie hello SAS, jeśli powinien być zagrożone.

Hello poniższy przykład tworzy zasady dostępu współdzielonego w udziale, a następnie używa, że zasady tooprovide hello ograniczenia na sygnatury dostępu Współdzielonego w pliku w hello udostępniać.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Aby uzyskać więcej informacji na temat tworzenia i używania sygnatur dostępu współdzielonego, zobacz artykuły [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego (SAS)) oraz [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md) (Tworzenie i używanie sygnatury dostępu współdzielonego w Magazynie obiektów Azure Blob).

## <a name="copy-files"></a>Kopiowanie plików
Począwszy od wersji 5.x hello biblioteki klienta magazynu Azure, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob. W kolejnych sekcjach hello przedstawiony, jak tooperform je skopiować operacji programowo.

Umożliwia także AzCopy toocopy jeden plik tooanother lub toocopy obiektu blob tooa pliku ani na odwrót. Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

> [!NOTE]
> Jeśli kopiujesz plik tooa obiektów blob lub obiektu blob tooa pliku, należy użyć dostępu współdzielonego sygnatury dostępu Współdzielonego tooauthenticate hello obiektu źródłowego, nawet jeśli kopiujesz w hello same konta magazynu.
> 
> 

**Skopiuj plik tooanother pliku** hello Poniższy przykładowy kod kopiuje plik tooanother pliku w hello samego udziału. Ponieważ ta operacja kopiowania plików w hello tego samego konta magazynu, możesz użyć kopii hello tooperform uwierzytelniania klucza wspólnego.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Skopiuj plik obiektu blob tooa** hello poniższy przykład tworzy plik i kopiuje go obiektu blob tooa w ramach hello tego samego konta magazynu. przykład Witaj tworzy sygnatury dostępu Współdzielonego dla pliku źródłowego hello, które usługa hello używa pliku źródłowego toohello dostępu tooauthenticate podczas operacji kopiowania hello.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

Można skopiować pliku blob tooa hello tak samo. Jeśli obiekt źródłowy hello jest obiektem blob, Utwórz obiektu blob toothat SAS tooauthenticate dostępu podczas operacji kopiowania hello.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Rozwiązywanie problemów z usługą Azure File Storage przy użyciu metryk
Funkcja analizy usługi Azure Storage obsługuje teraz metryki na potrzeby usługi Azure File Storage. Dane metryk umożliwiają śledzenie żądań i diagnozowanie problemów.


Można włączyć metryki dla usługi Magazyn plików Azure hello [Azure Portal](https://portal.azure.com). Można też włączyć je programowo przez hello wywołanie operacji ustawiania właściwości usługi plików za pośrednictwem interfejsu API REST hello lub jednej z analogicznych w hello biblioteki klienta usługi Storage.


Witaj poniższy przykład kodu pokazuje, jak toouse hello biblioteki klienta usługi Storage dla platformy .NET tooenable metryki dla usługi Magazyn plików Azure.

Najpierw dodaj następujące hello `using` tooyour dyrektywy `Program.cs` plików dodatkowo toothose dodanych wcześniej:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Należy pamiętać, że podczas obiektów blob Azure, Azure tabel i kolejek Azure Użyj udostępnionych hello `ServiceProperties` typu w hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` przestrzeni nazw, Magazyn plików Azure ma swój własny typ hello `FileServiceProperties` typu w hello `Microsoft.WindowsAzure.Storage.File.Protocol` przestrzeni nazw. Obu tych przestrzeni nazw musi odwoływać się w kodzie, jednak dla następującego kodu toocompile hello.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

Ponadto można odwoływać się za[magazyn plików Azure Rozwiązywanie problemów z artykułu](storage-troubleshoot-file-connection-problems.md) end-to-end wskazówki dotyczące rozwiązywania problemów.

## <a name="next-steps"></a>Następne kroki
Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.

### <a name="conceptual-articles-and-videos"></a>Artykuły koncepcyjne i filmy
* [Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)
* [Jak toouse magazyn plików Azure z systemem Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Narzędzia dostępne dla usługi Magazyn plików
* [Używanie programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md)
* [Jak toouse AzCopy z usługi Magazyn Microsoft Azure](storage-use-azcopy.md)
* [Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage](storage-azure-cli.md#create-and-manage-file-shares)
* [Rozwiązywanie problemów z usługą Azure File Storage](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Dokumentacja
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dokumentacja interfejsu API REST usługi plików](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Wpisy na blogach
* [Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)
* [Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)
* [Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)
* [Utrwalanie połączeń tooMicrosoft magazyn plików Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
