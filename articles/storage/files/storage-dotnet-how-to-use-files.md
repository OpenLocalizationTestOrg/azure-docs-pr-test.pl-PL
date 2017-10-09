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
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="d1f06-103">Tworzenie oprogramowania dla usługi Azure File Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d1f06-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="d1f06-104">W tym artykule przedstawiono sposób toomanage magazyn plików Azure z kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="d1f06-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="d1f06-105">toolearn więcej informacji na temat usługi Magazyn plików Azure, zobacz hello [tooAzure wprowadzenie magazyn plików](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1f06-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="d1f06-106">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="d1f06-106">About this tutorial</span></span>
<span data-ttu-id="d1f06-107">W tym samouczku przedstawiono podstawy hello przy użyciu platformy .NET toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f06-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="d1f06-108">W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem .NET i plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d1f06-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="d1f06-109">Pobierz hello zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="d1f06-109">Get hello contents of a file</span></span>
* <span data-ttu-id="d1f06-110">Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="d1f06-111">Utwórz sygnaturę dostępu współdzielonego (SAS klucza) dla pliku, która używa zasad dostępu współdzielonego zdefiniowanych w udziale hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="d1f06-112">Skopiuj plik tooanother pliku hello tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="d1f06-113">Skopiuj plik obiektu blob tooa hello tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="d1f06-114">Rozwiązywanie problemów przy użyciu metryk usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d1f06-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="d1f06-115">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure hello przy użyciu standardowych klas System.IO powitania dla operacji We/Wy pliku.</span><span class="sxs-lookup"><span data-stu-id="d1f06-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="d1f06-116">W tym artykule opisano, jak toowrite aplikacji, które używają hello Azure magazynu .NET SDK, który używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="d1f06-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="d1f06-117">Tworzenie aplikacji konsoli hello i uzyskiwanie zestawu hello</span><span class="sxs-lookup"><span data-stu-id="d1f06-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="d1f06-118">W programie Visual Studio utwórz nową aplikację konsoli dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d1f06-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="d1f06-119">Hello następujące kroki pokazują, jak toocreate aplikacji konsoli w programie Visual Studio 2017, jednak hello kroki są podobne w innych wersjach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1f06-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="d1f06-120">Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**</span><span class="sxs-lookup"><span data-stu-id="d1f06-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="d1f06-121">Wybierz kolejno pozycje **Zainstalowane** > **Szablony** > **Visual C#** > **Klasyczny pulpit systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="d1f06-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="d1f06-122">Wybierz pozycję **Aplikacja konsoli (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="d1f06-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="d1f06-123">Wprowadź nazwę aplikacji w hello **Name:** pola</span><span class="sxs-lookup"><span data-stu-id="d1f06-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="d1f06-124">Kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="d1f06-124">Select **OK**</span></span>

<span data-ttu-id="d1f06-125">Wszystkie przykłady kodu, w tym samouczku można dodać toohello `Main()` metody Aplikacja konsoli `Program.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="d1f06-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="d1f06-126">Można użyć hello biblioteki klienta magazynu Azure w dowolnego typu aplikacji .NET, w tym chmury Azure usługi lub aplikacji sieci web oraz aplikacje komputerów stacjonarnych i przenośnych.</span><span class="sxs-lookup"><span data-stu-id="d1f06-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="d1f06-127">W tym przewodniku dla uproszczenia przedstawiono aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="d1f06-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="d1f06-128">Korzystanie z pakietów hello wymagane tooinstall NuGet</span><span class="sxs-lookup"><span data-stu-id="d1f06-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="d1f06-129">Istnieją dwa pakiety tooreference toocomplete Twojego projektu musi w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="d1f06-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="d1f06-130">[Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ten pakiet zapewnia dostęp programistyczny toodata zasobów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="d1f06-131">[Biblioteka programu Microsoft Azure Configuration Manager dla środowiska .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): ten pakiet zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji, niezależnie od tego, gdzie została uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="d1f06-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="d1f06-132">Możesz użyć NuGet tooobtain oba pakiety.</span><span class="sxs-lookup"><span data-stu-id="d1f06-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="d1f06-133">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d1f06-133">Follow these steps:</span></span>

1. <span data-ttu-id="d1f06-134">Kliknij projekt prawym przyciskiem myszy w **Eksploratorze rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d1f06-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="d1f06-135">Wyszukaj w trybie online "Windowsazure.Storage", a następnie kliknij przycisk **zainstalować** tooinstall hello biblioteki klienta usługi Storage oraz jej zależności.</span><span class="sxs-lookup"><span data-stu-id="d1f06-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="d1f06-136">Wyszukaj w trybie online "WindowsAzure.ConfigurationManager", a następnie kliknij przycisk **zainstalować** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d1f06-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="d1f06-137">Zapisz plik app.config toohello poświadczeń konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d1f06-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="d1f06-138">Teraz zapiszemy poświadczenia w pliku app.config projektu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="d1f06-139">Edytowanie pliku app.config hello wygląda tak, jakby toohello podobnie poniższy przykład, zastępując `myaccount` z nazwę konta magazynu i `mykey` kluczem konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> najnowszą wersję Hello hello emulatora magazynu Azure nie obsługuje usługi Magazyn plików Azure. <span data-ttu-id="d1f06-141">Parametry połączenia muszą wskazywać konto magazynu Azure w hello toowork chmury z magazynem plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f06-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="d1f06-142">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="d1f06-142">Add using directives</span></span>
<span data-ttu-id="d1f06-143">Otwórz hello `Program.cs` plików w Eksploratorze rozwiązań i dodaj następujące hello przy użyciu dyrektywy toohello górnej części pliku hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="d1f06-144">Udział plików hello dostępu programowo</span><span class="sxs-lookup"><span data-stu-id="d1f06-144">Access hello file share programmatically</span></span>
<span data-ttu-id="d1f06-145">Następnie dodaj hello następującego kodu toohello `Main()` ciąg połączenia hello tooretrieve — metoda (po kodzie hello pokazanym powyżej).</span><span class="sxs-lookup"><span data-stu-id="d1f06-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="d1f06-146">Ten kod pobiera odwołanie do pliku toohello utworzonego wcześniej i wyświetla okno konsoli toohello jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="d1f06-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

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

<span data-ttu-id="d1f06-147">Uruchom dane wyjściowe hello toosee hello konsoli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1f06-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="d1f06-148">Ustaw maksymalny rozmiar hello udziału plików</span><span class="sxs-lookup"><span data-stu-id="d1f06-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="d1f06-149">Począwszy od wersji 5.x biblioteki klienta magazynu Azure hello, można skonfigurować zestaw hello przydziału (lub maksymalny rozmiar) udziału plików w gigabajtach.</span><span class="sxs-lookup"><span data-stu-id="d1f06-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="d1f06-150">Można również sprawdzić, jak dużo danych jest obecnie przechowywanych w udziale hello toosee.</span><span class="sxs-lookup"><span data-stu-id="d1f06-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="d1f06-151">Przez ustawienie hello limitu przydziału dla udziału można ograniczyć całkowity rozmiar plików hello przechowywanych w udziale hello hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="d1f06-152">Jeśli całkowity rozmiar plików w udziale hello hello przekracza przydział hello ustawiony na powitania udziału, a następnie klienci będą tooincrease hello rozmiaru istniejących plików lub tworzenia nowych plików, chyba że te pliki są puste.</span><span class="sxs-lookup"><span data-stu-id="d1f06-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="d1f06-153">w poniższym przykładzie Hello pokazuje, jak toocheck hello bieżące użycie udziału oraz jak tooset hello przydziału udziału hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="d1f06-154">Generowanie sygnatury dostępu współdzielonego dla pliku lub udziału plików</span><span class="sxs-lookup"><span data-stu-id="d1f06-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="d1f06-155">Począwszy od wersji 5.x hello biblioteki klienta magazynu Azure, można wygenerować sygnaturę dostępu współdzielonego (SAS) dla udziału plików lub dla pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="d1f06-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="d1f06-156">Można również tworzyć zasady dostępu współużytkowanego na dostęp do udostępnionych toomanage udziału plików podpisy.</span><span class="sxs-lookup"><span data-stu-id="d1f06-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="d1f06-157">Tworzenie zasad dostępu współdzielonego jest zalecane, ponieważ umożliwia cofnięcie hello SAS, jeśli powinien być zagrożone.</span><span class="sxs-lookup"><span data-stu-id="d1f06-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="d1f06-158">Hello poniższy przykład tworzy zasady dostępu współdzielonego w udziale, a następnie używa, że zasady tooprovide hello ograniczenia na sygnatury dostępu Współdzielonego w pliku w hello udostępniać.</span><span class="sxs-lookup"><span data-stu-id="d1f06-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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

<span data-ttu-id="d1f06-159">Aby uzyskać więcej informacji na temat tworzenia i używania sygnatur dostępu współdzielonego, zobacz artykuły [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) (Używanie sygnatur dostępu współdzielonego (SAS)) oraz [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md) (Tworzenie i używanie sygnatury dostępu współdzielonego w Magazynie obiektów Azure Blob).</span><span class="sxs-lookup"><span data-stu-id="d1f06-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="d1f06-160">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="d1f06-160">Copy files</span></span>
<span data-ttu-id="d1f06-161">Począwszy od wersji 5.x hello biblioteki klienta magazynu Azure, można skopiować pliku tooanother, obiektu blob tooa pliku lub pliku tooa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d1f06-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="d1f06-162">W kolejnych sekcjach hello przedstawiony, jak tooperform je skopiować operacji programowo.</span><span class="sxs-lookup"><span data-stu-id="d1f06-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="d1f06-163">Umożliwia także AzCopy toocopy jeden plik tooanother lub toocopy obiektu blob tooa pliku ani na odwrót.</span><span class="sxs-lookup"><span data-stu-id="d1f06-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="d1f06-164">Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1f06-164">See [Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="d1f06-165">Jeśli kopiujesz plik tooa obiektów blob lub obiektu blob tooa pliku, należy użyć dostępu współdzielonego sygnatury dostępu Współdzielonego tooauthenticate hello obiektu źródłowego, nawet jeśli kopiujesz w hello same konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="d1f06-166">**Skopiuj plik tooanother pliku** hello Poniższy przykładowy kod kopiuje plik tooanother pliku w hello samego udziału.</span><span class="sxs-lookup"><span data-stu-id="d1f06-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="d1f06-167">Ponieważ ta operacja kopiowania plików w hello tego samego konta magazynu, możesz użyć kopii hello tooperform uwierzytelniania klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="d1f06-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

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

<span data-ttu-id="d1f06-168">**Skopiuj plik obiektu blob tooa** hello poniższy przykład tworzy plik i kopiuje go obiektu blob tooa w ramach hello tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d1f06-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="d1f06-169">przykład Witaj tworzy sygnatury dostępu Współdzielonego dla pliku źródłowego hello, które usługa hello używa pliku źródłowego toohello dostępu tooauthenticate podczas operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

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

<span data-ttu-id="d1f06-170">Można skopiować pliku blob tooa hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="d1f06-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="d1f06-171">Jeśli obiekt źródłowy hello jest obiektem blob, Utwórz obiektu blob toothat SAS tooauthenticate dostępu podczas operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="d1f06-172">Rozwiązywanie problemów z usługą Azure File Storage przy użyciu metryk</span><span class="sxs-lookup"><span data-stu-id="d1f06-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="d1f06-173">Funkcja analizy usługi Azure Storage obsługuje teraz metryki na potrzeby usługi Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="d1f06-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="d1f06-174">Dane metryk umożliwiają śledzenie żądań i diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="d1f06-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="d1f06-175">Można włączyć metryki dla usługi Magazyn plików Azure hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1f06-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="d1f06-176">Można też włączyć je programowo przez hello wywołanie operacji ustawiania właściwości usługi plików za pośrednictwem interfejsu API REST hello lub jednej z analogicznych w hello biblioteki klienta usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="d1f06-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="d1f06-177">Witaj poniższy przykład kodu pokazuje, jak toouse hello biblioteki klienta usługi Storage dla platformy .NET tooenable metryki dla usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f06-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="d1f06-178">Najpierw dodaj następujące hello `using` tooyour dyrektywy `Program.cs` plików dodatkowo toothose dodanych wcześniej:</span><span class="sxs-lookup"><span data-stu-id="d1f06-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="d1f06-179">Należy pamiętać, że podczas obiektów blob Azure, Azure tabel i kolejek Azure Użyj udostępnionych hello `ServiceProperties` typu w hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` przestrzeni nazw, Magazyn plików Azure ma swój własny typ hello `FileServiceProperties` typu w hello `Microsoft.WindowsAzure.Storage.File.Protocol` przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d1f06-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="d1f06-180">Obu tych przestrzeni nazw musi odwoływać się w kodzie, jednak dla następującego kodu toocompile hello.</span><span class="sxs-lookup"><span data-stu-id="d1f06-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

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

<span data-ttu-id="d1f06-181">Ponadto można odwoływać się za[magazyn plików Azure Rozwiązywanie problemów z artykułu](storage-troubleshoot-windows-file-connection-problems.md) end-to-end wskazówki dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="d1f06-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1f06-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1f06-182">Next steps</span></span>
<span data-ttu-id="d1f06-183">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f06-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="d1f06-184">Artykuły koncepcyjne i filmy</span><span class="sxs-lookup"><span data-stu-id="d1f06-184">Conceptual articles and videos</span></span>
* <span data-ttu-id="d1f06-185">[Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)</span><span class="sxs-lookup"><span data-stu-id="d1f06-185">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="d1f06-186">Jak toouse magazyn plików Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="d1f06-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="d1f06-187">Narzędzia dostępne dla usługi Magazyn plików</span><span class="sxs-lookup"><span data-stu-id="d1f06-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="d1f06-188">Jak toouse AzCopy z usługi Magazyn Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d1f06-188">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="d1f06-189">Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d1f06-189">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="d1f06-190">Rozwiązywanie problemów z usługą Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="d1f06-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="d1f06-191">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="d1f06-191">Reference</span></span>
* [<span data-ttu-id="d1f06-192">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="d1f06-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="d1f06-193">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="d1f06-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="d1f06-194">Wpisy na blogach</span><span class="sxs-lookup"><span data-stu-id="d1f06-194">Blog posts</span></span>
* <span data-ttu-id="d1f06-195">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)</span><span class="sxs-lookup"><span data-stu-id="d1f06-195">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)</span></span>
* <span data-ttu-id="d1f06-196">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="d1f06-196">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* <span data-ttu-id="d1f06-197">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="d1f06-197">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)</span></span>
* [<span data-ttu-id="d1f06-198">Utrwalanie połączeń tooMicrosoft magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="d1f06-198">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
