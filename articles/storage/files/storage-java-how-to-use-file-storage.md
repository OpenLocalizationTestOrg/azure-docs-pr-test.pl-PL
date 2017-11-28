---
title: "aaaDevelop Azure File Storage z językiem Java | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dane plików toodevelop Java aplikacji i usług, które używają toostore magazyn plików Azure."
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
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="7d151-103">Tworzenie dla usługi Magazyn plików Azure z językiem Java</span><span class="sxs-lookup"><span data-stu-id="7d151-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="7d151-104">Informacje o tym samouczku</span><span class="sxs-lookup"><span data-stu-id="7d151-104">About this tutorial</span></span>
<span data-ttu-id="7d151-105">W tym samouczku przedstawiono podstawy hello za pomocą języka Java toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="7d151-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="7d151-106">W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem Java i plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="7d151-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="7d151-107">Tworzenie i usuwanie udziałów plików Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="7d151-108">Tworzenie i usuwanie katalogów</span><span class="sxs-lookup"><span data-stu-id="7d151-108">Create and delete directories</span></span>
* <span data-ttu-id="7d151-109">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="7d151-110">Przekazywanie, pobieranie i usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="7d151-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="7d151-111">Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure hello przy użyciu standardowych klas Java we/wy hello.</span><span class="sxs-lookup"><span data-stu-id="7d151-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="7d151-112">W tym artykule opisano, jak toowrite aplikacji, które używają hello SDK Java magazynu Azure, która używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="7d151-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="7d151-113">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="7d151-113">Create a Java application</span></span>
<span data-ttu-id="7d151-114">Przykłady hello toobuild, konieczne będzie hello Java Development Kit (JDK) i hello [Azure Storage SDK for Java] [].</span><span class="sxs-lookup"><span data-stu-id="7d151-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="7d151-115">Należy również utworzono konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d151-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="7d151-116">Instalator programu toouse aplikacji usługi Magazyn plików Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="7d151-117">Witaj toouse magazynu Azure interfejsów API, Dodaj powitania po instrukcji toohello górnej części pliku Java hello, w którym ma tooaccess hello magazynu usługi z.</span><span class="sxs-lookup"><span data-stu-id="7d151-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="7d151-118">Konfiguracja parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="7d151-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="7d151-119">toouse magazyn plików Azure, musisz mieć konto magazynu Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7d151-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7d151-120">Witaj pierwszym krokiem będzie tooconfigure parametry połączenia, które będą używane konto magazynu tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="7d151-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="7d151-121">Umożliwia definiowanie statycznego toodo zmiennej który.</span><span class="sxs-lookup"><span data-stu-id="7d151-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="7d151-122">Zamień your_storage_account_name i your_storage_account_key hello rzeczywiste wartości dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7d151-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="7d151-123">Łączenie z kontem magazynu platformy Azure tooan</span><span class="sxs-lookup"><span data-stu-id="7d151-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="7d151-124">tooconnect tooyour konta magazynu, należy toouse hello **CloudStorageAccount** przekazania tooits ciąg połączenia obiektu **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="7d151-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="7d151-125">**CloudStorageAccount.parse** zwraca InvalidKeyException, dlatego potrzebujesz tooput zablokować go w programie try/catch.</span><span class="sxs-lookup"><span data-stu-id="7d151-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="7d151-126">Tworzenie udziału plików platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-126">Create an Azure File share</span></span>
<span data-ttu-id="7d151-127">Wszystkich plików i katalogów w usłudze magazyn plików Azure znajdują się w kontenerze o nazwie **udziału**.</span><span class="sxs-lookup"><span data-stu-id="7d151-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="7d151-128">Twoje konto magazynu może mieć tyle udziałów zezwala pojemności Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="7d151-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="7d151-129">tooobtain dostępu tooa udziału i jego zawartość, należy toouse klienta magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="7d151-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="7d151-130">Za pomocą klienta magazyn plików Azure hello można następnie uzyskać udziału tooa odwołania.</span><span class="sxs-lookup"><span data-stu-id="7d151-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="7d151-131">tooactually utworzyć udział hello, użyj hello **createIfNotExists** metody hello CloudFileShare obiektu.</span><span class="sxs-lookup"><span data-stu-id="7d151-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="7d151-132">W tym momencie **udostępnianie** posiada udział tooa odwołania o nazwie **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="7d151-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="7d151-133">Usuń udział plików Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-133">Delete an Azure File share</span></span>
<span data-ttu-id="7d151-134">Usuwanie udziału jest realizowane przez wywołanie hello **deleteIfExists** metody dla obiekt CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="7d151-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="7d151-135">Oto przykładowy kod, który robi to.</span><span class="sxs-lookup"><span data-stu-id="7d151-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="7d151-136">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="7d151-136">Create a directory</span></span>
<span data-ttu-id="7d151-137">Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="7d151-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="7d151-138">Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów, jako Twoje konto zostanie.</span><span class="sxs-lookup"><span data-stu-id="7d151-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="7d151-139">Poniższy kod Hello utworzy podkatalogu o nazwie **sampledir** w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="7d151-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="7d151-140">Usuwanie katalogu</span><span class="sxs-lookup"><span data-stu-id="7d151-140">Delete a directory</span></span>
<span data-ttu-id="7d151-141">Usunięcie katalogu jest dość proste zadania, jednak należy zauważyć, że nie można usunąć katalogu, w którym nadal zawiera pliki lub katalogi innych.</span><span class="sxs-lookup"><span data-stu-id="7d151-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="7d151-142">Wyliczanie plików i katalogów w udziale plików Azure</span><span class="sxs-lookup"><span data-stu-id="7d151-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="7d151-143">Uzyskiwanie listy plików i katalogów w udziale łatwo odbywa się przez wywołanie metody **listFilesAndDirectories** na odwołanie CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="7d151-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="7d151-144">Metoda Hello zwraca listę ListFileItem obiektów, które można wykonać iterację na.</span><span class="sxs-lookup"><span data-stu-id="7d151-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="7d151-145">Na przykład hello następujący kod będzie zawierała listę plików i katalogów w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="7d151-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="7d151-146">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="7d151-146">Upload a file</span></span>
<span data-ttu-id="7d151-147">Plik Azure, który zawiera na powitania bardzo najmniej udziału, katalog główny, w którym mogą znajdować się pliki.</span><span class="sxs-lookup"><span data-stu-id="7d151-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="7d151-148">W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.</span><span class="sxs-lookup"><span data-stu-id="7d151-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="7d151-149">pierwszym krokiem Hello przekazywania pliku jest tooobtain katalogu toohello odwołania, gdzie powinien znajdować się.</span><span class="sxs-lookup"><span data-stu-id="7d151-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="7d151-150">W tym celu wywoływania hello **getRootDirectoryReference** metody hello udziału obiektu.</span><span class="sxs-lookup"><span data-stu-id="7d151-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="7d151-151">Teraz, gdy masz katalog główny odwołania toohello hello udziału, możesz przekazać plik na przy użyciu następującego kodu hello.</span><span class="sxs-lookup"><span data-stu-id="7d151-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="7d151-152">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="7d151-152">Download a file</span></span>
<span data-ttu-id="7d151-153">Jednym z hello częstsze operacje, które będą wykonywane względem usługi Magazyn plików Azure jest toodownload plików.</span><span class="sxs-lookup"><span data-stu-id="7d151-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="7d151-154">W hello poniższy przykład hello kod pobiera SampleFile.txt i wyświetla jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="7d151-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="7d151-155">Usuwanie pliku</span><span class="sxs-lookup"><span data-stu-id="7d151-155">Delete a file</span></span>
<span data-ttu-id="7d151-156">Inna operacja magazynu plików Azure wspólnej jest usuwanie plików.</span><span class="sxs-lookup"><span data-stu-id="7d151-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="7d151-157">Witaj następujący kod usuwa plik o nazwie SampleFile.txt przechowywany w katalogu o nazwie **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="7d151-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="7d151-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d151-158">Next steps</span></span>
<span data-ttu-id="7d151-159">Jeśli chcesz toolearn więcej informacji na temat innych interfejsów API magazynu Azure, skorzystaj z poniższych linków.</span><span class="sxs-lookup"><span data-stu-id="7d151-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="7d151-160">[Azure dla deweloperów języka Java](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="7d151-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="7d151-161">Magazyn Azure SDK dla języka Java</span><span class="sxs-lookup"><span data-stu-id="7d151-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="7d151-162">Magazyn Azure SDK dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="7d151-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="7d151-163">Odwołanie do zestawu SDK klienta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7d151-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="7d151-164">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7d151-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="7d151-165">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7d151-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="7d151-166">[Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="7d151-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>