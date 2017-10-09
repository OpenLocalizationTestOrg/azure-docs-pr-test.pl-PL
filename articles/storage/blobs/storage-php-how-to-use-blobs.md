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
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Jak toouse obiektu blob magazynu w języku PHP
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

Ten przewodnik przedstawia, jak usługa blob tooperform typowych scenariuszy przy użyciu hello Azure. Przykłady Hello są zapisywane w kodzie PHP i używają hello [zestaw Azure SDK for PHP][download]. Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob. Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz hello [następne kroki](#next-steps) sekcji.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Tworzenie aplikacji PHP
Witaj tylko do tworzenia aplikacji PHP, który uzyskuje dostęp do usługi Azure blob hello wymaganiem hello odwołuje się do klas w hello Azure SDK for PHP z w kodzie. Można użyć dowolnego toocreate narzędzi rozwoju aplikacji, łącznie z Notatnika.

W tym przewodniku należy użyć funkcji usługi, które można wywołać w ramach aplikacji PHP lokalnie lub w kodzie działających w roli sieci web platformy Azure, roli procesu roboczego lub witryny sieci Web.

## <a name="get-hello-azure-client-libraries"></a>Pobierz bibliotek klienckich hello Azure
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Konfigurowanie usługi blob hello tooaccess aplikacji
usługi obiektów blob platformy Azure hello toouse interfejsów API, musisz:

1. Plik automatycznej ładowarki hello odwołania przy użyciu hello [require_once] instrukcji, i
2. Odwoływać się do wszystkich klas, których może używać.

Witaj poniższy przykład przedstawia sposób tooinclude hello hello plików i odwołanie automatycznej ładowarki **ServicesBuilder** klasy.

> [!NOTE]
> Przykłady Hello w tym artykule przyjęto założenie, że zainstalowano hello bibliotek klienckich PHP na platformie Azure za pośrednictwem Composer. Biblioteki hello zainstalować ręcznie, konieczne będzie tooreference hello `WindowsAzure.php` automatycznej ładowarki pliku.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

W poniższych przykładach hello, hello `require_once` instrukcji będą wyświetlane zawsze, ale odwołuje się tylko hello klasy niezbędne do tooexecute przykład hello.

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
tooinstantiate klient usługi obiektów blob platformy Azure, musisz najpierw mieć prawidłowe parametry połączenia. Hello format dla parametrów połączenia usługi blob hello jest:

Aby uzyskać dostęp do usługi na żywo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Aby uzyskać dostęp do emulatora magazynu hello:

```php
UseDevelopmentStorage=true
```

toocreate dowolnego klienta usługi Azure należy toouse hello **ServicesBuilder** klasy. Możesz:

* Przekaż połączenia hello ciągu bezpośrednio tooit lub
* Użyj hello **CloudConfigurationManager (CCM)** toocheck zewnętrzne wiele źródeł dla parametrów połączenia hello:
  * Domyślnie pochodzi z obsługą jednego źródła zewnętrznego — zmiennych środowiskowych.
  * Można dodać nowych źródeł, rozszerzając hello **ConnectionStringSource** klasy.

Przykłady hello opisana w tym temacie hello parametry połączenia zostaną przekazane bezpośrednio.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Tworzenie kontenera
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** obiektu umożliwia tworzenie kontenera obiektów blob z hello **tworzony kontener** metody. Podczas tworzenia kontenera, można ustawić opcje w kontenerze hello, ale spowoduje to nie jest wymagane. (hello poniższy przykład pokazuje, jak tooset hello kontenera uzyskiwać dostęp formantu listy (ACL) i metadanych kontenera.)

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

Wywoływanie **setPublicAccess (PublicAccessType::CONTAINER\_i\_obiektów blob)** sprawia, że hello dostępny za pomocą żądań anonimowych danych i obiektów blob kontenera. Wywoływanie **setPublicAccess(PublicAccessType::BLOBS_ONLY)** sprawia, że tylko obiektu blob danych dostępny za pomocą żądań anonimowych. Aby uzyskać więcej informacji na temat kontenera listy kontroli dostępu, zobacz [kontenera zestawu list kontroli dostępu (interfejsu API REST)][container-acl].

Aby uzyskać więcej informacji o kodach błędów usługi obiektów Blob, zobacz [kody błędów usługi Blob][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
tooupload pliku jako obiekt blob, użyj hello **BlobRestProxy -> createBlockBlob** metody. Ta operacja tworzy hello obiektu blob nie istnieje lub zastąpiony, jeśli istnieje. Hello poniższy przykład kodu zakłada kontenera hello została już utworzona i używa [fopen —] [ fopen] tooopen hello pliku jako strumień.

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

Należy pamiętać, że hello powyższego przykładu przekazywanie obiektu blob jako strumień. Jednak obiektu blob również mogą być przekazywane jako ciągu przy użyciu, na przykład hello [pliku\_uzyskać\_zawartość] [ file_get_contents] funkcji. toodo to przy użyciu powyższego przykładu hello Zmień `$content = fopen("c:\myfile.txt", "r");` zbyt`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, użyj hello **BlobRestProxy -> listBlobs** metody z **foreach** tooloop za pośrednictwem wyników z hello w pętli. Witaj poniższy kod wyświetla nazwę hello każdy obiekt blob jako dane wyjściowe w kontenerze oraz przeglądarki toohello jego identyfikatora URI.

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

## <a name="download-a-blob"></a>Pobieranie obiektu blob
toodownload obiektu blob hello wywołania **BlobRestProxy -> getBlob** metody, a następnie wywołania hello **getContentStream** metody na powitania wynikowa **GetBlobResult** obiektu.

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

Należy zauważyć, że ten przykład Witaj powyżej pobiera obiektu blob jako zasób strumienia (hello domyślne zachowanie). Można jednak użyć hello [strumienia\_uzyskać\_zawartość] [ stream-get-contents] hello tooconvert funkcja zwrócony ciąg tooa strumienia.

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
toodelete obiektu blob, Przekaż hello nazwa kontenera i nazwa obiektu blob zbyt**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Usunięcie kontenera obiektów blob
Na koniec toodelete kontenera obiektów blob, Przekaż nazwa kontenera hello zbyt**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi obiektów blob platformy Azure, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* Odwiedź hello [blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Zobacz hello [PHP blokowych obiektów blob przykład](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Zobacz hello [przykład obiektu blob strony PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
