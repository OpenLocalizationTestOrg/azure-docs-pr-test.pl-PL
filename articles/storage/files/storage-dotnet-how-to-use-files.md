---
title: "Tworzenie oprogramowania dla usługi Azure File Storage przy użyciu platformy .NET | Microsoft Docs"
description: "Dowiedz się, jak opracować aplikacje platformy .NET i usługi korzystające z usługi Azure File Storage do przechowywania plików danych."
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
ms.openlocfilehash: 7b94e70619324bb8dc8e7f8306f00f06e7476c1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="44d46-103">Tworzenie oprogramowania dla usługi Azure File Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="44d46-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="44d46-104">W tym artykule przedstawiono sposób zarządzania usługą Azure File Storage za pomocą kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="44d46-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="44d46-105">Aby dowiedzieć się więcej na temat usługi Azure File Storage, zobacz artykuł [Introduction to Azure File storage](storage-files-introduction.md) (Wprowadzenie do usługi Azure File Storage).</span><span class="sxs-lookup"><span data-stu-id="44d46-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="44d46-106">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="44d46-106">About this tutorial</span></span>
<span data-ttu-id="44d46-107">W tym samouczku przedstawiono podstawy korzystania z platformy .NET do tworzenia aplikacji lub usług, które korzystają z usługi Azure File Storage do przechowywania danych plików.</span><span class="sxs-lookup"><span data-stu-id="44d46-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="44d46-108">W tym samouczku utworzymy prostą aplikację konsolową i pokażemy, jak wykonywać podstawowe działania za pomocą platformy .NET i usługi Azure File Storage:</span><span class="sxs-lookup"><span data-stu-id="44d46-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="44d46-109">Pobieranie zawartości pliku</span><span class="sxs-lookup"><span data-stu-id="44d46-109">Get the contents of a file</span></span>
* <span data-ttu-id="44d46-110">Ustawienie limitu przydziału (maksymalnego rozmiaru) udziału plików.</span><span class="sxs-lookup"><span data-stu-id="44d46-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="44d46-111">Utworzenie sygnatury dostępu współdzielonego (klucza SAS) dla pliku, która używa zasad dostępu współdzielonego zdefiniowanych w udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="44d46-112">Skopiowanie pliku do innego pliku w tym samym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="44d46-113">Skopiowanie pliku do obiektu blob w tym samym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="44d46-114">Rozwiązywanie problemów przy użyciu metryk usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="44d46-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="44d46-115">Dostęp do usługi Azure File Storage można uzyskiwać za pośrednictwem protokołu SMB i dlatego istnieje możliwość napisania prostej aplikacji, która uzyskuje plikowy dostęp we/wy do udziału plików platformy Azure przy użyciu standardowych klas System.IO.</span><span class="sxs-lookup"><span data-stu-id="44d46-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="44d46-116">W tym artykule opisano sposób pisania aplikacji, które używają zestawu .NET SDK usługi Azure Storage korzystającego z [interfejsu API REST magazynu plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) w celu komunikowania się z usługą Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="44d46-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="44d46-117">Tworzenie aplikacji konsolowej i uzyskiwanie zestawu</span><span class="sxs-lookup"><span data-stu-id="44d46-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="44d46-118">W programie Visual Studio utwórz nową aplikację konsoli dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="44d46-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="44d46-119">Poniższe kroki pokazują, jak utworzyć aplikację konsoli w programie Visual Studio 2017, jednak kroki w innych wersjach programu Visual Studio są podobne.</span><span class="sxs-lookup"><span data-stu-id="44d46-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="44d46-120">Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**</span><span class="sxs-lookup"><span data-stu-id="44d46-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="44d46-121">Wybierz kolejno pozycje **Zainstalowane** > **Szablony** > **Visual C#** > **Klasyczny pulpit systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="44d46-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="44d46-122">Wybierz pozycję **Aplikacja konsoli (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="44d46-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="44d46-123">Wprowadź nazwę aplikacji w polu **Nazwa:**</span><span class="sxs-lookup"><span data-stu-id="44d46-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="44d46-124">Kliknij przycisk **OK**</span><span class="sxs-lookup"><span data-stu-id="44d46-124">Select **OK**</span></span>

<span data-ttu-id="44d46-125">Wszystkie przykłady kodu w tym samouczku można dodać do metody `Main()` w pliku `Program.cs` aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="44d46-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="44d46-126">Biblioteki klienta usługi Azure Storage można używać w aplikacjach .NET dowolnego typu , m.in. usługach w chmurze lub aplikacjach sieci Web platformy Azure, aplikacjach pulpitu i aplikacjach mobilnych.</span><span class="sxs-lookup"><span data-stu-id="44d46-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="44d46-127">W tym przewodniku dla uproszczenia przedstawiono aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="44d46-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="44d46-128">Użycie pakietu NuGet w celu zainstalowania wymaganych pakietów</span><span class="sxs-lookup"><span data-stu-id="44d46-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="44d46-129">Istnieją dwa pakiety, które trzeba przywołać w projekcie, aby ukończyć ten samouczek:</span><span class="sxs-lookup"><span data-stu-id="44d46-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="44d46-130">[Biblioteka klienta usługi Storage platformy Microsoft Azure dla środowiska .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ten pakiet zapewnia dostęp programowy do zasobów danych na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="44d46-131">[Biblioteka programu Microsoft Azure Configuration Manager dla środowiska .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): ten pakiet zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji, niezależnie od tego, gdzie została uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="44d46-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="44d46-132">Pakiet NuGet służy do pobrania obu pakietów.</span><span class="sxs-lookup"><span data-stu-id="44d46-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="44d46-133">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44d46-133">Follow these steps:</span></span>

1. <span data-ttu-id="44d46-134">Kliknij projekt prawym przyciskiem myszy w **Eksploratorze rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="44d46-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="44d46-135">Wyszukaj w trybie online ciąg „WindowsAzure.Storage”, a następnie kliknij przycisk **Zainstaluj**, aby zainstalować Bibliotekę klienta usługi Storage oraz jej zależności.</span><span class="sxs-lookup"><span data-stu-id="44d46-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="44d46-136">Wyszukaj w trybie online ciąg „WindowsAzure.ConfigurationManager” i kliknij przycisk **Zainstaluj**, aby zainstalować program Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="44d46-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="44d46-137">Zapisywanie poświadczeń konta magazynu w pliku app.config</span><span class="sxs-lookup"><span data-stu-id="44d46-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="44d46-138">Teraz zapiszemy poświadczenia w pliku app.config projektu.</span><span class="sxs-lookup"><span data-stu-id="44d46-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="44d46-139">Zmodyfikuj plik app.config, jak pokazano w poniższym przykładzie, zastępując ciąg `myaccount` nazwą konta magazynu, a ciąg `mykey` kluczem konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> Najnowsza wersja emulatora magazynu Azure nie obsługuje usługi Azure File Storage. <span data-ttu-id="44d46-141">Aby można było pracować z usługą Azure File Storage, parametry połączenia muszą wskazywać konto usługi Azure Storage w chmurze.</span><span class="sxs-lookup"><span data-stu-id="44d46-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="44d46-142">Dodawanie dyrektyw using</span><span class="sxs-lookup"><span data-stu-id="44d46-142">Add using directives</span></span>
<span data-ttu-id="44d46-143">Otwórz plik `Program.cs` w Eksploratorze rozwiązań i dodaj następujące dyrektywy using na początku pliku.</span><span class="sxs-lookup"><span data-stu-id="44d46-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="44d46-144">Programowy dostęp do udziału plików</span><span class="sxs-lookup"><span data-stu-id="44d46-144">Access the file share programmatically</span></span>
<span data-ttu-id="44d46-145">Teraz dodamy poniższy kod do metody `Main()` (po kodzie pokazanym powyżej) w celu pobrania parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="44d46-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="44d46-146">Ten kod pobiera odwołanie do pliku utworzonego wcześniej i wyświetla jego zawartość w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="44d46-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="44d46-147">Aby zobaczyć dane wyjściowe, uruchom aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="44d46-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="44d46-148">Ustawianie maksymalnego rozmiaru udziału plików</span><span class="sxs-lookup"><span data-stu-id="44d46-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="44d46-149">Począwszy od wersji 5.x biblioteki klienta usługi Azure Storage, można ustawić limit przydziału (lub maksymalny rozmiar) udziału plików w gigabajtach.</span><span class="sxs-lookup"><span data-stu-id="44d46-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="44d46-150">Można również sprawdzić, ile danych jest obecnie przechowywanych w udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="44d46-151">Ustawiając limit przydziału dla udziału, można ograniczyć całkowity rozmiar plików przechowywanych w udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="44d46-152">Jeśli całkowity rozmiar plików w udziale przekroczy ustawiony limit przydziału, klienci nie będą mogli zwiększyć rozmiaru istniejących plików ani tworzyć nowych plików (chyba że pliki będą puste).</span><span class="sxs-lookup"><span data-stu-id="44d46-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="44d46-153">W poniższym przykładzie pokazano, jak sprawdzić bieżące użycie udziału oraz jak ustawić limit przydziału w udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="44d46-154">Generowanie sygnatury dostępu współdzielonego dla pliku lub udziału plików</span><span class="sxs-lookup"><span data-stu-id="44d46-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="44d46-155">Począwszy od wersji 5.x biblioteki klienta usługi Azure Storage, można wygenerować sygnaturę dostępu współdzielonego dla udziału plików lub dla pojedynczego pliku.</span><span class="sxs-lookup"><span data-stu-id="44d46-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="44d46-156">Można też utworzyć zasady dostępu współdzielonego w udziale plików na potrzeby zarządzania sygnaturami dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="44d46-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="44d46-157">Utworzenie zasad dostępu współdzielonego jest zalecane, ponieważ umożliwia cofnięcie sygnatur w przypadku zagrożenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="44d46-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="44d46-158">W poniższym przykładzie tworzone są zasady dostępu współdzielonego w udziale. Następnie za pomocą tych zasad nakładane są ograniczenia na sygnatury dostępu współdzielonego w pliku w udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="44d46-159">Aby uzyskać więcej informacji na temat tworzenia i używania sygnatur dostępu współdzielonego, zobacz artykuły [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) (Używanie sygnatur dostępu współdzielonego (SAS)) oraz [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md) (Tworzenie i używanie sygnatury dostępu współdzielonego w Magazynie obiektów Azure Blob).</span><span class="sxs-lookup"><span data-stu-id="44d46-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="44d46-160">Kopiowanie plików</span><span class="sxs-lookup"><span data-stu-id="44d46-160">Copy files</span></span>
<span data-ttu-id="44d46-161">Począwszy od wersji 5.x biblioteki klienta usługi Azure Storage, można kopiować pliki do innych plików, pliki do obiektów blob oraz obiekty blob do plików.</span><span class="sxs-lookup"><span data-stu-id="44d46-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="44d46-162">W kolejnych sekcjach pokażemy, jak programowo wykonywać te operacje kopiowania.</span><span class="sxs-lookup"><span data-stu-id="44d46-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="44d46-163">Do kopiowania plików do innych plików oraz obiektów blob do plików i odwrotnie można także użyć narzędzia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="44d46-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="44d46-164">Zobacz: [Transfer danych za pomocą narzędzia wiersza polecenia AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44d46-164">See [Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="44d46-165">W przypadku kopiowania obiektu blob do pliku lub pliku do obiektu blob konieczne jest uwierzytelnienie obiektu źródłowego za pomocą sygnatury dostępu współdzielonego, nawet jeśli kopiowanie odbywa się w ramach tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="44d46-166">**Kopiowanie pliku do innego pliku** Poniższy przykładowy kod powoduje skopiowanie pliku do innego pliku w tym samym udziale.</span><span class="sxs-lookup"><span data-stu-id="44d46-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="44d46-167">Ponieważ ta operacja kopiowania jest wykonywana w ramach tego samego konta magazynu, można użyć uwierzytelniania przy użyciu klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="44d46-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="44d46-168">**Kopiowanie pliku do obiektu blob** Poniższy przykładowy kod powoduje utworzenie pliku i skopiowanie go do obiektu blob w ramach tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="44d46-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="44d46-169">Dla pliku źródłowego tworzona jest sygnatura dostępu współdzielonego, za pomocą której usługa uwierzytelnia dostęp do tego pliku podczas operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="44d46-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="44d46-170">W ten sam sposób można skopiować obiekt blob do pliku.</span><span class="sxs-lookup"><span data-stu-id="44d46-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="44d46-171">Jeśli obiekt źródłowy jest obiektem blob, utwórz sygnaturę dostępu współdzielonego w celu uwierzytelniania dostępu do tego obiektu blob podczas operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="44d46-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="44d46-172">Rozwiązywanie problemów z usługą Azure File Storage przy użyciu metryk</span><span class="sxs-lookup"><span data-stu-id="44d46-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="44d46-173">Funkcja analizy usługi Azure Storage obsługuje teraz metryki na potrzeby usługi Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="44d46-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="44d46-174">Dane metryk umożliwiają śledzenie żądań i diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="44d46-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="44d46-175">Metryki dla usługi Azure File Storage można włączyć w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d46-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="44d46-176">Można też włączyć je programowo przez wywołanie operacji ustawiania właściwości usługi plików za pomocą interfejsu API REST lub przy użyciu jednej z analogicznych operacji w bibliotece klienta usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="44d46-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="44d46-177">Poniższy przykładowy kod pokazuje, jak włączyć metryki dla usługi Azure File Storage za pomocą biblioteki klienta usługi Storage programu .NET.</span><span class="sxs-lookup"><span data-stu-id="44d46-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="44d46-178">Najpierw dodaj następujące dyrektywy `using` do pliku `Program.cs` (obok tych dodanych powyżej):</span><span class="sxs-lookup"><span data-stu-id="44d46-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="44d46-179">Zwróć uwagę, że usługi Blob Storage, Table Storage i Queue Storage używają wspólnie typu `ServiceProperties` w przestrzeni nazw `Microsoft.WindowsAzure.Storage.Shared.Protocol`, natomiast usługa File Storage ma swój własny typ `FileServiceProperties` w przestrzeni nazw `Microsoft.WindowsAzure.Storage.File.Protocol`.</span><span class="sxs-lookup"><span data-stu-id="44d46-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="44d46-180">Jednak aby można było skompilować poniższy kod, musi on zawierać odwołania do obu tych przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="44d46-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

<span data-ttu-id="44d46-181">Aby uzyskać kompleksowe wskazówki dotyczące rozwiązywania problemów, można zajrzeć do [artykułu na temat rozwiązywania problemów z usługą Azure File Storage](storage-troubleshoot-windows-file-connection-problems.md).</span><span class="sxs-lookup"><span data-stu-id="44d46-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d46-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44d46-182">Next steps</span></span>
<span data-ttu-id="44d46-183">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="44d46-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="44d46-184">Artykuły koncepcyjne i filmy</span><span class="sxs-lookup"><span data-stu-id="44d46-184">Conceptual articles and videos</span></span>
* <span data-ttu-id="44d46-185">[Azure File Storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Azure File Storage: płynnie działający system plików SMB w chmurze dla systemów Windows i Linux)</span><span class="sxs-lookup"><span data-stu-id="44d46-185">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* <span data-ttu-id="44d46-186">[How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) (Jak używać usługi Azure File Storage z systemem Linux)</span><span class="sxs-lookup"><span data-stu-id="44d46-186">[How to use Azure File storage with Linux](storage-how-to-use-files-linux.md)</span></span>

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="44d46-187">Narzędzia dostępne dla usługi Magazyn plików</span><span class="sxs-lookup"><span data-stu-id="44d46-187">Tooling support for File storage</span></span>
* <span data-ttu-id="44d46-188">[How to use AzCopy with Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) (Jak używać narzędzia AzCopy z usługą Microsoft Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="44d46-188">[How to use AzCopy with Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)</span></span>
* [<span data-ttu-id="44d46-189">Używanie interfejsu wiersza polecenia platformy Azure z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="44d46-189">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="44d46-190">Rozwiązywanie problemów z usługą Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="44d46-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="44d46-191">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="44d46-191">Reference</span></span>
* [<span data-ttu-id="44d46-192">Dokumentacja biblioteki klienta usługi Storage dla programu .NET</span><span class="sxs-lookup"><span data-stu-id="44d46-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="44d46-193">Dokumentacja interfejsu API REST usługi plików</span><span class="sxs-lookup"><span data-stu-id="44d46-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="44d46-194">Wpisy na blogach</span><span class="sxs-lookup"><span data-stu-id="44d46-194">Blog posts</span></span>
* <span data-ttu-id="44d46-195">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/) (Usługa Azure File Storage została udostępniona publicznie)</span><span class="sxs-lookup"><span data-stu-id="44d46-195">[Azure File storage is now generally available](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)</span></span>
* <span data-ttu-id="44d46-196">[Inside Azure File Storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Za kulisami usługi Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="44d46-196">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* <span data-ttu-id="44d46-197">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx) (Wprowadzenie do usługi plików platformy Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="44d46-197">[Introducing Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)</span></span>
* <span data-ttu-id="44d46-198">[Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx) (Utrwalanie połączeń z usługą Microsoft Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="44d46-198">[Persisting connections to Microsoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)</span></span>