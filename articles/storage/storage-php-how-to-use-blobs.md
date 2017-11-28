---
title: "Jak używać magazynu obiektów blob (obiekt magazynu) za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="e1470-103">Jak używać magazynu obiektów blob w języku PHP</span><span class="sxs-lookup"><span data-stu-id="e1470-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="e1470-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e1470-104">Overview</span></span>
<span data-ttu-id="e1470-105">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e1470-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="e1470-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1470-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="e1470-107">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="e1470-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="e1470-108">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1470-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="e1470-109">Przykłady są napisane w PHP i użyj [zestaw Azure SDK for PHP][download].</span><span class="sxs-lookup"><span data-stu-id="e1470-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="e1470-110">Omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e1470-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="e1470-111">Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e1470-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="e1470-112">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="e1470-112">Create a PHP application</span></span>
<span data-ttu-id="e1470-113">Jedynym wymaganiem służący do tworzenia aplikacji PHP, który uzyskuje dostęp do usług obiektów blob platformy Azure jest odwoływanie się do klasy w zestawie SDK Azure dla programu PHP z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e1470-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="e1470-114">Narzędzia do programowania służy do tworzenia aplikacji, łącznie z Notatnika.</span><span class="sxs-lookup"><span data-stu-id="e1470-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="e1470-115">W tym przewodniku należy użyć funkcji usługi, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e1470-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="e1470-116">Pobierz bibliotek klienta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e1470-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="e1470-117">Konfigurowanie aplikacji do uzyskania dostępu do usługi blob</span><span class="sxs-lookup"><span data-stu-id="e1470-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="e1470-118">Aby korzystać z usługi Azure blob interfejsów API, musisz:</span><span class="sxs-lookup"><span data-stu-id="e1470-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="e1470-119">Odwołanie przy użyciu pliku automatycznej ładowarki [require_once] instrukcji, i</span><span class="sxs-lookup"><span data-stu-id="e1470-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="e1470-120">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="e1470-120">Reference any classes you might use.</span></span>

<span data-ttu-id="e1470-121">Poniższy przykład pokazuje, jak dołączyć plik automatycznej ładowarki i odwołanie **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="e1470-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="e1470-122">Przykłady w tym artykule przyjęto założenie, że zainstalowano bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="e1470-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="e1470-123">Jeśli zainstalowano bibliotek ręcznie, należy odwoływać się do `WindowsAzure.php` automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="e1470-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="e1470-124">W poniższych przykładach `require_once` instrukcji będą wyświetlane zawsze, ale odwołuje się tylko do klas, które są konieczne na przykład do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e1470-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e1470-125">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="e1470-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="e1470-126">Można utworzyć klienta usługi obiektów blob platformy Azure, najpierw musi mieć prawidłowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="e1470-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="e1470-127">Format dla parametrów połączenia usługi obiektów blob jest:</span><span class="sxs-lookup"><span data-stu-id="e1470-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="e1470-128">Aby uzyskać dostęp do usługi na żywo:</span><span class="sxs-lookup"><span data-stu-id="e1470-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="e1470-129">Aby uzyskać dostęp do emulatora magazynu:</span><span class="sxs-lookup"><span data-stu-id="e1470-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="e1470-130">Aby utworzyć dowolnego klienta usługi Azure, musisz użyć **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="e1470-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="e1470-131">Możesz:</span><span class="sxs-lookup"><span data-stu-id="e1470-131">You can:</span></span>

* <span data-ttu-id="e1470-132">Przekaż parametry połączenia do niego bezpośrednio lub</span><span class="sxs-lookup"><span data-stu-id="e1470-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="e1470-133">Użyj **CloudConfigurationManager (CCM)** do sprawdzenia wiele źródeł zewnętrznych ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="e1470-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="e1470-134">Domyślnie pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="e1470-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="e1470-135">Można dodać nowego źródła rozszerzając **ConnectionStringSource** klasy.</span><span class="sxs-lookup"><span data-stu-id="e1470-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="e1470-136">Przykłady przedstawione w tym miejscu parametry połączenia zostaną przekazane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e1470-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="e1470-137">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="e1470-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="e1470-138">A **BlobRestProxy** obiektu umożliwia tworzenie kontenera obiektów blob z **tworzony kontener** metody.</span><span class="sxs-lookup"><span data-stu-id="e1470-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="e1470-139">Podczas tworzenia kontenera, można ustawić opcje w kontenerze, ale spowoduje to nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="e1470-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="e1470-140">(W poniższym przykładzie pokazano sposób ustawiania listy kontroli dostępu do kontenera (ACL) i metadanych kontenera).</span><span class="sxs-lookup"><span data-stu-id="e1470-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e1470-141">Wywoływanie **setPublicAccess (PublicAccessType::CONTAINER\_i\_obiektów blob)** powoduje, że dane i kontener obiektów blob jest dostępny za pomocą żądań anonimowych.</span><span class="sxs-lookup"><span data-stu-id="e1470-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="e1470-142">Wywoływanie **setPublicAccess(PublicAccessType::BLOBS_ONLY)** sprawia, że tylko obiektu blob danych dostępny za pomocą żądań anonimowych.</span><span class="sxs-lookup"><span data-stu-id="e1470-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="e1470-143">Aby uzyskać więcej informacji na temat kontenera listy kontroli dostępu, zobacz [kontenera zestawu list kontroli dostępu (interfejsu API REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="e1470-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="e1470-144">Aby uzyskać więcej informacji o kodach błędów usługi obiektów Blob, zobacz [kody błędów usługi Blob][error-codes].</span><span class="sxs-lookup"><span data-stu-id="e1470-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e1470-145">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="e1470-145">Upload a blob into a container</span></span>
<span data-ttu-id="e1470-146">Aby przekazać plik jako obiekt blob, użyj **BlobRestProxy -> createBlockBlob** metody.</span><span class="sxs-lookup"><span data-stu-id="e1470-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="e1470-147">Ta operacja tworzy obiektu blob nie istnieje lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="e1470-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="e1470-148">W poniższym przykładzie kodu zakłada, że kontener został już utworzony i używa [fopen —] [ fopen] można otworzyć pliku jako strumień.</span><span class="sxs-lookup"><span data-stu-id="e1470-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e1470-149">Należy pamiętać, że powyższego przykładu przekazywanie obiektu blob jako strumień.</span><span class="sxs-lookup"><span data-stu-id="e1470-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="e1470-150">Jednak obiektu blob mogą również być przekazywane jako przy użyciu ciągu, na przykład [pliku\_uzyskać\_zawartość] [ file_get_contents] funkcji.</span><span class="sxs-lookup"><span data-stu-id="e1470-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="e1470-151">Aby to zrobić przy użyciu powyższego przykładu, zmień `$content = fopen("c:\myfile.txt", "r");` do `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="e1470-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="e1470-152">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="e1470-152">List the blobs in a container</span></span>
<span data-ttu-id="e1470-153">Aby wyświetlić listę obiektów blob w kontenerze, należy użyć **BlobRestProxy -> listBlobs** metody z **foreach** pętlę do pętli za pośrednictwem wyniku.</span><span class="sxs-lookup"><span data-stu-id="e1470-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="e1470-154">Poniższy kod wyświetla nazwę każdego obiektu blob jako dane wyjściowe w kontenerze oraz jego identyfikatora URI do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="e1470-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="e1470-155">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="e1470-155">Download a blob</span></span>
<span data-ttu-id="e1470-156">Aby pobrać obiektu blob, należy wywołać **BlobRestProxy -> getBlob** metody, następnie wywołaj **getContentStream** metoda powstałe w ten sposób **GetBlobResult** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e1470-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="e1470-157">Należy pamiętać, że w powyższym przykładzie pobiera obiektu blob jako zasób strumienia (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="e1470-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="e1470-158">Można jednak użyć [strumienia\_uzyskać\_zawartość] [ stream-get-contents] funkcji konwersji na ciąg zwrócony strumień.</span><span class="sxs-lookup"><span data-stu-id="e1470-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="e1470-159">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="e1470-159">Delete a blob</span></span>
<span data-ttu-id="e1470-160">Aby usunąć obiekt blob, Przekaż nazwa kontenera i nazwa obiektu blob do **BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="e1470-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="e1470-161">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e1470-161">Delete a blob container</span></span>
<span data-ttu-id="e1470-162">Na koniec można usunąć kontenera obiektów blob, przekaż nazwę kontenera, aby **BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="e1470-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="e1470-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1470-163">Next steps</span></span>
<span data-ttu-id="e1470-164">Teraz, kiedy znasz już podstawy usługi Azure blob, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="e1470-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="e1470-165">Odwiedź stronę [blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="e1470-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="e1470-166">Zobacz [PHP blokowych obiektów blob przykład](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="e1470-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="e1470-167">Zobacz [przykład obiektu blob strony PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="e1470-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="e1470-168">Transfer danych za pomocą narzędzia wiersza polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="e1470-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="e1470-169">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="e1470-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="e1470-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="e1470-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
