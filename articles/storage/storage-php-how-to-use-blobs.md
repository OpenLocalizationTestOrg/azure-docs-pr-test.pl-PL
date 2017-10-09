---
title: "aaaHow toouse obiektu blob magazynu (obiekt) za pomocą języka PHP | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="27d0b-103">Jak toouse obiektu blob magazynu w języku PHP</span><span class="sxs-lookup"><span data-stu-id="27d0b-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="27d0b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="27d0b-104">Overview</span></span>
<span data-ttu-id="27d0b-105">Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="27d0b-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="27d0b-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27d0b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="27d0b-107">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="27d0b-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="27d0b-108">Ten przewodnik przedstawia, jak usługa blob tooperform typowych scenariuszy przy użyciu hello Azure.</span><span class="sxs-lookup"><span data-stu-id="27d0b-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="27d0b-109">Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP][download].</span><span class="sxs-lookup"><span data-stu-id="27d0b-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="27d0b-110">Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="27d0b-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="27d0b-111">Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz hello [następne kroki](#next-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="27d0b-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="27d0b-112">Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="27d0b-112">Create a PHP application</span></span>
<span data-ttu-id="27d0b-113">Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure blob hello wymaganiem hello odwołuje się do klas w hello Azure SDK for PHP z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="27d0b-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="27d0b-114">Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.</span><span class="sxs-lookup"><span data-stu-id="27d0b-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="27d0b-115">W tym przewodniku należy użyć funkcji usługi, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="27d0b-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="27d0b-116">Pobierz bibliotek klienckich hello Azure</span><span class="sxs-lookup"><span data-stu-id="27d0b-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="27d0b-117">Konfigurowanie usługi blob hello tooaccess aplikacji</span><span class="sxs-lookup"><span data-stu-id="27d0b-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="27d0b-118">usługi obiektów blob platformy Azure hello toouse interfejsów API, musisz:</span><span class="sxs-lookup"><span data-stu-id="27d0b-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="27d0b-119">Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] instrukcji, i</span><span class="sxs-lookup"><span data-stu-id="27d0b-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="27d0b-120">Odwoływać się do wszystkich klas, których może używać.</span><span class="sxs-lookup"><span data-stu-id="27d0b-120">Reference any classes you might use.</span></span>

<span data-ttu-id="27d0b-121">Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="27d0b-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="27d0b-122">Przykłady Hello w tym artykule przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer.</span><span class="sxs-lookup"><span data-stu-id="27d0b-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="27d0b-123">Biblioteki hello zainstalować ręcznie, konieczne będzie tooreference hello `WindowsAzure.php` automatycznej ładowarki pliku.</span><span class="sxs-lookup"><span data-stu-id="27d0b-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="27d0b-124">W poniższych przykładach hello, hello `require_once` instrukcji będą wyświetlane zawsze, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.</span><span class="sxs-lookup"><span data-stu-id="27d0b-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="27d0b-125">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="27d0b-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="27d0b-126">tooinstantiate klient usługi obiektów blob platformy Azure, musisz najpierw mieć prawidłowe parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="27d0b-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="27d0b-127">Hello format dla parametrów połączenia usługi blob hello jest:</span><span class="sxs-lookup"><span data-stu-id="27d0b-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="27d0b-128">Aby uzyskać dostęp do usługi na żywo:</span><span class="sxs-lookup"><span data-stu-id="27d0b-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="27d0b-129">Aby uzyskać dostęp do emulatora magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="27d0b-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="27d0b-130">toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy.</span><span class="sxs-lookup"><span data-stu-id="27d0b-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="27d0b-131">Możesz:</span><span class="sxs-lookup"><span data-stu-id="27d0b-131">You can:</span></span>

* <span data-ttu-id="27d0b-132">Przekaż połączenia hello ciągu bezpośrednio tooit lub</span><span class="sxs-lookup"><span data-stu-id="27d0b-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="27d0b-133">Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="27d0b-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="27d0b-134">Domyślnie pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="27d0b-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="27d0b-135">Można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** klasy.</span><span class="sxs-lookup"><span data-stu-id="27d0b-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="27d0b-136">Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="27d0b-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="27d0b-137">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="27d0b-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="27d0b-138">A **BlobRestProxy** obiektu umożliwia tworzenie kontenera obiektów blob z hello **tworzony kontener** metody.</span><span class="sxs-lookup"><span data-stu-id="27d0b-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="27d0b-139">Podczas tworzenia kontenera, można ustawić opcje w kontenerze hello, ale spowoduje to nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="27d0b-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="27d0b-140">(hello poniższy przykład pokazuje, jak tooset hello kontenera uzyskiwać dostęp formantu listy (ACL) i metadanych kontenera.)</span><span class="sxs-lookup"><span data-stu-id="27d0b-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="27d0b-141">Wywoływanie **setPublicAccess (PublicAccessType::CONTAINER\_i\_obiektów blob)** sprawia, że hello dostępny za pomocą żądań anonimowych danych i obiektów blob kontenera.</span><span class="sxs-lookup"><span data-stu-id="27d0b-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="27d0b-142">Wywoływanie **setPublicAccess(PublicAccessType::BLOBS_ONLY)** sprawia, że tylko obiektu blob danych dostępny za pomocą żądań anonimowych.</span><span class="sxs-lookup"><span data-stu-id="27d0b-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="27d0b-143">Aby uzyskać więcej informacji na temat kontenera listy kontroli dostępu, zobacz [kontenera zestawu list kontroli dostępu (interfejsu API REST)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="27d0b-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="27d0b-144">Aby uzyskać więcej informacji o kodach błędów usługi obiektów Blob, zobacz [kody błędów usługi Blob][error-codes].</span><span class="sxs-lookup"><span data-stu-id="27d0b-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="27d0b-145">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="27d0b-145">Upload a blob into a container</span></span>
<span data-ttu-id="27d0b-146">tooupload pliku jako obiekt blob, użyj hello **BlobRestProxy -> createBlockBlob** metody.</span><span class="sxs-lookup"><span data-stu-id="27d0b-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="27d0b-147">Ta operacja tworzy hello obiektu blob nie istnieje lub zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="27d0b-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="27d0b-148">Hello poniższy przykład kodu zakłada kontenera hello została już utworzona i używa [fopen —] [ fopen] tooopen hello pliku jako strumień.</span><span class="sxs-lookup"><span data-stu-id="27d0b-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="27d0b-149">Należy pamiętać, że hello powyższego przykładu przekazywanie obiektu blob jako strumień.</span><span class="sxs-lookup"><span data-stu-id="27d0b-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="27d0b-150">Jednak obiektu blob również mogą być przekazywane jako ciągu przy użyciu, na przykład hello [pliku\_uzyskać\_zawartość] [ file_get_contents] funkcji.</span><span class="sxs-lookup"><span data-stu-id="27d0b-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="27d0b-151">toodo to przy użyciu powyższego przykładu hello Zmień `$content = fopen("c:\myfile.txt", "r");` zbyt`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="27d0b-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="27d0b-152">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="27d0b-152">List hello blobs in a container</span></span>
<span data-ttu-id="27d0b-153">toolist hello BLOB w kontenerze, użyj hello **BlobRestProxy -> listBlobs** metody z **foreach** tooloop za pośrednictwem wyników z hello w pętli.</span><span class="sxs-lookup"><span data-stu-id="27d0b-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="27d0b-154">Witaj poniższy kod wyświetla nazwę hello każdy obiekt blob jako dane wyjściowe w kontenerze oraz przeglądarki toohello jego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="27d0b-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="27d0b-155">Pobieranie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="27d0b-155">Download a blob</span></span>
<span data-ttu-id="27d0b-156">toodownload obiektu blob hello wywołania **BlobRestProxy -> getBlob** metody, a następnie wywołania hello **getContentStream** metody na powitania wynikowa **GetBlobResult** obiektu.</span><span class="sxs-lookup"><span data-stu-id="27d0b-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="27d0b-157">Należy zauważyć, że ten przykład Witaj powyżej pobiera obiektu blob jako zasób strumienia (hello domyślne zachowanie).</span><span class="sxs-lookup"><span data-stu-id="27d0b-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="27d0b-158">Można jednak użyć hello [strumienia\_uzyskać\_zawartość] [ stream-get-contents] hello tooconvert funkcja zwrócony ciąg tooa strumienia.</span><span class="sxs-lookup"><span data-stu-id="27d0b-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="27d0b-159">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="27d0b-159">Delete a blob</span></span>
<span data-ttu-id="27d0b-160">toodelete obiektu blob, Przekaż hello nazwa kontenera i nazwa obiektu blob zbyt**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="27d0b-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="27d0b-161">Usunięcie kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="27d0b-161">Delete a blob container</span></span>
<span data-ttu-id="27d0b-162">Na koniec toodelete kontenera obiektów blob, Przekaż nazwa kontenera hello zbyt**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="27d0b-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="27d0b-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="27d0b-163">Next steps</span></span>
<span data-ttu-id="27d0b-164">Teraz, kiedy znasz już podstawy hello hello usługi obiektów blob platformy Azure, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="27d0b-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="27d0b-165">Odwiedź hello [blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="27d0b-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="27d0b-166">Zobacz hello [PHP blokowych obiektów blob przykład](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="27d0b-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="27d0b-167">Zobacz hello [przykład obiektu blob strony PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="27d0b-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="27d0b-168">Transfer danych za pomocą wiersza polecenia Azcopy hello</span><span class="sxs-lookup"><span data-stu-id="27d0b-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="27d0b-169">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="27d0b-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
