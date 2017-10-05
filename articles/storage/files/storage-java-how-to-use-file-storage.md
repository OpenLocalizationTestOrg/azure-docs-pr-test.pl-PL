---
title: "Tworzenie dla usługi Magazyn plików Azure z językiem Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzenie aplikacji Java i usługami korzystającymi z usługi Magazyn plików Azure do przechowywania plików danych."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: ce38944b9d5e663505c5808864ba61a5e2284f3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="73f51-103">Tworzenie dla usługi Magazyn plików Azure z językiem Java</span><span class="sxs-lookup"><span data-stu-id="73f51-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="73f51-104">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="73f51-104">About this tutorial</span></span>
<span data-ttu-id="73f51-105">W tym samouczku przedstawiono podstawy do tworzenia aplikacji lub usługi, które korzystają z usługi Magazyn plików Azure do przechowywania danych plików za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="73f51-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="73f51-106">W tym samouczku utworzymy prostej aplikacji konsolowej ją i pokazują, jak wykonywać podstawowe działania z magazynem Java i plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="73f51-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="73f51-107">Tworzenie i usuwanie udziałów plików Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="73f51-108">Tworzenie i usuwanie katalogów</span><span class="sxs-lookup"><span data-stu-id="73f51-108">Create and delete directories</span></span>
* <span data-ttu-id="73f51-109">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="73f51-110">Przekazywanie, pobieranie i usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="73f51-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="73f51-111">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, istnieje możliwość zapisu proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure przy użyciu standardowych klas Java we/wy.</span><span class="sxs-lookup"><span data-stu-id="73f51-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="73f51-112">W tym artykule opisano sposób pisania aplikacji, które używają SDK Java magazynu Azure, która używa [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) aby komunikował się z usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="73f51-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="73f51-113">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="73f51-113">Create a Java application</span></span>
<span data-ttu-id="73f51-114">Aby utworzyć próbek, konieczne będzie Java Development Kit (JDK) i [] [Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="73f51-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="73f51-115">Należy również utworzono konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73f51-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="73f51-116">Instalowanie aplikacji do używania usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="73f51-117">Aby używać interfejsów API magazynu Azure, dodaj następującą instrukcję na początku pliku języka Java, gdy chcesz uzyskać dostęp do usługi magazynu z.</span><span class="sxs-lookup"><span data-stu-id="73f51-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="73f51-118">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="73f51-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="73f51-119">Aby korzystać z usługi Magazyn plików Azure, należy nawiązać połączenia z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73f51-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="73f51-120">Pierwszym krokiem jest skonfigurowanie parametrów połączenia, które będą używane do łączenia się z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="73f51-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="73f51-121">Umożliwia zdefiniowanie zmienną statyczną, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="73f51-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="73f51-122">Zamień your_storage_account_name i your_storage_account_key rzeczywiste wartości dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="73f51-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="73f51-123">Łączenie z kontem magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="73f51-124">Do łączenia się z kontem magazynu, należy użyć **CloudStorageAccount** parametry połączenia do przekazania obiektu jego **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="73f51-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="73f51-125">**CloudStorageAccount.parse** InvalidKeyException zgłasza wyjątek, dlatego należy go umieścić wewnątrz bloku try/catch.</span><span class="sxs-lookup"><span data-stu-id="73f51-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="73f51-126">Tworzenie udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-126">Create an Azure File share</span></span>
<span data-ttu-id="73f51-127">Wszystkich plików i katalogów w usłudze magazyn plików Azure znajdują się w kontenerze o nazwie **udziału**.</span><span class="sxs-lookup"><span data-stu-id="73f51-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="73f51-128">Twoje konto magazynu może mieć tyle udziałów zezwala pojemności Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="73f51-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="73f51-129">Aby uzyskać dostęp do udziału i jego zawartość, musisz użyć klienta magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="73f51-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="73f51-130">Za pomocą klienta magazyn plików Azure można następnie uzyskać odwołania do udziału.</span><span class="sxs-lookup"><span data-stu-id="73f51-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="73f51-131">Aby rzeczywiście utworzyć udział, użyj **createIfNotExists** metody CloudFileShare obiektu.</span><span class="sxs-lookup"><span data-stu-id="73f51-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="73f51-132">W tym momencie **udostępnianie** zawiera odwołanie do udziału o nazwie **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="73f51-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="73f51-133">Usuń udział plików Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-133">Delete an Azure File share</span></span>
<span data-ttu-id="73f51-134">Usuwanie udziału odbywa się przez wywołanie metody **deleteIfExists** metody dla obiekt CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="73f51-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="73f51-135">Oto przykładowy kod, który robi to.</span><span class="sxs-lookup"><span data-stu-id="73f51-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="73f51-136">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="73f51-136">Create a directory</span></span>
<span data-ttu-id="73f51-137">Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="73f51-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="73f51-138">Magazyn plików Azure umożliwia tworzenie tyle katalogów dopuszcza Twoje konto.</span><span class="sxs-lookup"><span data-stu-id="73f51-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="73f51-139">Poniższy kod będzie utworzyć podkatalogu o nazwie **sampledir** w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="73f51-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="73f51-140">Usuwanie katalogu</span><span class="sxs-lookup"><span data-stu-id="73f51-140">Delete a directory</span></span>
<span data-ttu-id="73f51-141">Usunięcie katalogu jest dość proste zadania, jednak należy zauważyć, że nie można usunąć katalogu, w którym nadal zawiera pliki lub katalogi innych.</span><span class="sxs-lookup"><span data-stu-id="73f51-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="73f51-142">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="73f51-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="73f51-143">Uzyskiwanie listy plików i katalogów w udziale łatwo odbywa się przez wywołanie metody **listFilesAndDirectories** na odwołanie CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="73f51-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="73f51-144">Metoda zwraca listę ListFileItem obiekty, które można wykonać iterację na.</span><span class="sxs-lookup"><span data-stu-id="73f51-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="73f51-145">Na przykład następujący kod będzie zawierała listę plików i katalogów w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="73f51-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="73f51-146">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="73f51-146">Upload a file</span></span>
<span data-ttu-id="73f51-147">Plik Azure udział zawiera co najmniej, katalog główny, w którym mogą znajdować się pliki.</span><span class="sxs-lookup"><span data-stu-id="73f51-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="73f51-148">W tej sekcji dowiesz się, jak można przekazać pliku z magazynu lokalnego do katalogu głównego udziału.</span><span class="sxs-lookup"><span data-stu-id="73f51-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="73f51-149">Pierwszym krokiem podczas przekazywania pliku jest uzyskać odwołania do katalogu, której się znajduje.</span><span class="sxs-lookup"><span data-stu-id="73f51-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="73f51-150">Można to zrobić przez wywołanie metody **getRootDirectoryReference** metody obiektu udziału.</span><span class="sxs-lookup"><span data-stu-id="73f51-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="73f51-151">Teraz, gdy masz odwołania do katalogu głównego udziału, możesz przekazać plik na przy użyciu następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="73f51-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="73f51-152">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="73f51-152">Download a file</span></span>
<span data-ttu-id="73f51-153">Jednym z częstsze operacje, które będą wykonywane względem usługi Magazyn plików Azure jest do pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="73f51-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="73f51-154">W poniższym przykładzie kod pobiera SampleFile.txt i wyświetla jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="73f51-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="73f51-155">Usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="73f51-155">Delete a file</span></span>
<span data-ttu-id="73f51-156">Inna operacja magazynu plików Azure wspólnej jest usuwanie plików.</span><span class="sxs-lookup"><span data-stu-id="73f51-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="73f51-157">Poniższy kod usuwa plik o nazwie SampleFile.txt przechowywany w katalogu o nazwie **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="73f51-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="73f51-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73f51-158">Next steps</span></span>
<span data-ttu-id="73f51-159">Jeśli chcesz dowiedzieć się więcej o innych interfejsów API magazynu Azure, skorzystaj z poniższych linków.</span><span class="sxs-lookup"><span data-stu-id="73f51-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="73f51-160">[Azure dla deweloperów języka Java](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="73f51-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="73f51-161">Magazyn Azure SDK dla języka Java</span><span class="sxs-lookup"><span data-stu-id="73f51-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="73f51-162">Magazyn Azure SDK dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="73f51-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="73f51-163">Odwołanie do zestawu SDK klienta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="73f51-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="73f51-164">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="73f51-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="73f51-165">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="73f51-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="73f51-166">[Transfer danych za pomocą narzędzia wiersza polecenia AzCopy](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="73f51-166">[Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>