---
title: "Jak używać magazynu obiektów Blob platformy Azure (obiekt magazynu) w języku Java | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e4de1bc57adf668f383d1fbaf4a721a61576d2a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="f8039-103">Jak używać Magazynu obiektów Blob w języku Java</span><span class="sxs-lookup"><span data-stu-id="f8039-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="f8039-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f8039-104">Overview</span></span>
<span data-ttu-id="f8039-105">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="f8039-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f8039-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f8039-107">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="f8039-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="f8039-108">W tym artykule opisano sposób wykonywania typowych scenariuszy przy użyciu magazynu obiektów Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f8039-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="f8039-109">Przykłady są napisane w języku Java i użyj [Azure Storage SDK for Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="f8039-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="f8039-110">Omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="f8039-111">Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz [następne kroki](#Next-Steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="f8039-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="f8039-112">Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="f8039-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="f8039-113">Aby uzyskać więcej informacji, zobacz [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="f8039-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="f8039-114">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="f8039-114">Create a Java application</span></span>
<span data-ttu-id="f8039-115">W tym artykule użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f8039-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="f8039-116">Aby to zrobić, należy zainstalować zestaw Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8039-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="f8039-117">Po zostało to zrobione, należy sprawdzić, czy platformie programistycznej spełnia minimalne wymagania i zależności, które są wymienione w [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f8039-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="f8039-118">Jeżeli system spełnia te wymagania, należy wykonać instrukcje dotyczące pobierania i instalowania biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f8039-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="f8039-119">Po wykonaniu tych zadań, można utworzyć aplikacji Java, który używa przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f8039-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="f8039-120">Konfigurowanie aplikacji dostęp do magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="f8039-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="f8039-121">Dodaj następujące instrukcje import u góry pliku języka Java, którym chcesz uzyskać dostępu do obiektów blob przy użyciu interfejsów API magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="f8039-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="f8039-122">Konfigurowanie parametrów połączenia magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="f8039-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="f8039-123">Klient usługi Azure Storage używa parametrów połączenia magazynu do przechowywania punktów końcowych i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8039-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="f8039-124">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu w następującym formacie, przy użyciu nazwy konta magazynu i podstawowy klucz dostępu dla konta magazynu na liście [portalu Azure](https://portal.azure.com) dla *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="f8039-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="f8039-125">W poniższym przykładzie pokazano, jak można zadeklarować pola statycznego do przechowywania parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="f8039-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="f8039-126">W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi *pliku ServiceConfiguration.cscfg*i jest dostępny w wyniku wywołania **RoleEnvironment.getConfigurationSettings** metody.</span><span class="sxs-lookup"><span data-stu-id="f8039-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="f8039-127">Poniższy przykład pobiera parametry połączenia z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="f8039-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="f8039-128">Poniższe przykłady założono użycie jednej z tych dwóch metod można pobrać parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="f8039-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="f8039-129">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="f8039-129">Create a container</span></span>
<span data-ttu-id="f8039-130">A **CloudBlobClient** obiektu pozwala pobierać obiekty odwołań dla kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="f8039-131">Poniższy kod tworzy **CloudBlobClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f8039-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="f8039-132">Istnieją dodatkowe sposoby tworzenia **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w [odwołania do zestawu SDK klienta magazynu Azure].</span><span class="sxs-lookup"><span data-stu-id="f8039-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f8039-133">Użyj **CloudBlobClient** obiekt, aby pobrać odwołanie do kontenera, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="f8039-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="f8039-134">Kontener można utworzyć, jeśli nie istnieje z **createIfNotExists** metody, które w przeciwnym razie zwraca istniejącego kontenera.</span><span class="sxs-lookup"><span data-stu-id="f8039-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="f8039-135">Domyślnie nowy kontener jest prywatny, dlatego należy określić klucz dostępu do magazynu (tak samo jak wcześniej) aby pobierać obiekty BLOB z tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="f8039-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="f8039-136">Opcjonalnie: Konfigurowanie kontener dla dostępu publicznego</span><span class="sxs-lookup"><span data-stu-id="f8039-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="f8039-137">Kontener uprawnienia są domyślnie skonfigurowane dla dostępu prywatnego, ale można łatwo skonfigurować kontenera uprawnień umożliwiających dostęp do publicznego, tylko do odczytu dla wszystkich użytkowników w Internecie:</span><span class="sxs-lookup"><span data-stu-id="f8039-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f8039-138">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="f8039-138">Upload a blob into a container</span></span>
<span data-ttu-id="f8039-139">Aby przekazać pliku do obiektu blob, Pobierz odwołanie do kontenera i użyj go, aby pobrać odwołanie do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="f8039-140">Po utworzeniu odwołanie do obiektu blob możesz przekazać strumieniem, wywołując przekazywania na odwołanie do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="f8039-141">Ta operacja spowoduje utworzenie obiektu blob, jeśli nie istnieje lub jego zastąpienie, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="f8039-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="f8039-142">Poniższy przykład kodu pokazuje i przyjęto założenie, że kontener został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="f8039-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f8039-143">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="f8039-143">List the blobs in a container</span></span>
<span data-ttu-id="f8039-144">Aby wyświetlić listę obiektów blob w kontenerze, należy najpierw pobrać odwołanie do kontenera, jak przekazać obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="f8039-145">Korzystając z kontenera **listBlobs** metody z **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="f8039-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="f8039-146">Poniższy kod wyświetla identyfikator Uri każdy obiekt blob w kontenerze do konsoli.</span><span class="sxs-lookup"><span data-stu-id="f8039-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="f8039-147">Należy pamiętać, nazwę obiekty BLOB zawierające informacje o ścieżce ich nazw.</span><span class="sxs-lookup"><span data-stu-id="f8039-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="f8039-148">Powoduje to utworzenie wirtualnej struktury katalogów, które można organizować i przechodzić między nimi tak jak w przypadku tradycyjnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="f8039-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="f8039-149">Należy pamiętać, że struktura katalogów jest wyłącznie wirtualna — jedyne zasoby dostępne w Magazynie obiektów blob to kontenery i obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="f8039-150">Jednak biblioteka klienta oferuje **CloudBlobDirectory** obiekt, aby odwoływać się do katalogu wirtualnego i uprościć proces Praca z obiektami blob zorganizowanymi w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="f8039-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="f8039-151">Na przykład można mieć kontener o nazwie "zdjęć", w których może przekazać obiekty BLOB o nazwie "rootphoto1", "2010/photo1", "2010/photo2" i "2011/photo1".</span><span class="sxs-lookup"><span data-stu-id="f8039-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="f8039-152">Spowoduje to utworzenie katalogi wirtualne "2010" i "2011" w kontenerze "zdjęć".</span><span class="sxs-lookup"><span data-stu-id="f8039-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="f8039-153">Podczas wywoływania **listBlobs** w kontenerze "fotografie" Kolekcja zwracana będzie zawierać **CloudBlobDirectory** i **CloudBlob** obiekty reprezentujące katalogów i obiekty BLOB zawarte na najwyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="f8039-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="f8039-154">W takim przypadku katalogi "2010" i "2011", a także photo "rootphoto1" zostałaby zwrócona.</span><span class="sxs-lookup"><span data-stu-id="f8039-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="f8039-155">Można użyć **instanceof** operatora, aby odróżnić tych obiektów.</span><span class="sxs-lookup"><span data-stu-id="f8039-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="f8039-156">Opcjonalnie można przekazać parametry **listBlobs** metody z **useFlatBlobListing** parametr ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="f8039-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="f8039-157">Spowoduje to każdy obiekt blob zostały zwrócone, niezależnie od tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8039-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="f8039-158">Aby uzyskać więcej informacji, zobacz **CloudBlobContainer.listBlobs** w [odwołania do zestawu SDK klienta magazynu Azure].</span><span class="sxs-lookup"><span data-stu-id="f8039-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="f8039-159">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f8039-159">Download a blob</span></span>
<span data-ttu-id="f8039-160">Aby pobrać obiekty BLOB, wykonaj te same czynności, ponieważ została ona przekazywanie obiektu blob, aby pobrać odwołanie do obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="f8039-161">W przykładzie przekazywania przekazywania jest wywoływana dla obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f8039-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="f8039-162">W poniższym przykładzie, wywołanie pobierania, aby przesłać zawartość obiektu blob do obiektu strumienia, takich jak **FileOutputStream** można utrwalić obiektu blob do pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f8039-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="f8039-163">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="f8039-163">Delete a blob</span></span>
<span data-ttu-id="f8039-164">Aby usunąć obiekt blob, Pobierz odwołanie do obiektu blob i wywołanie **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="f8039-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="f8039-165">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f8039-165">Delete a blob container</span></span>
<span data-ttu-id="f8039-166">Na koniec można usunąć kontenera obiektów blob, Pobierz obiekt blob odwołanie do kontenera i wywołanie **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="f8039-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="f8039-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8039-167">Next steps</span></span>
<span data-ttu-id="f8039-168">Teraz, kiedy znasz już podstawy magazynu obiektów Blob, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="f8039-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="f8039-169">[Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="f8039-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="f8039-170">[Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołania do zestawu SDK klienta magazynu Azure]</span><span class="sxs-lookup"><span data-stu-id="f8039-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="f8039-171">[Interfejs API REST usługi Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="f8039-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="f8039-172">[Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="f8039-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="f8039-173">Aby uzyskać więcej informacji, zobacz też [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="f8039-173">For more information, see also [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołania do zestawu SDK klienta magazynu Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
