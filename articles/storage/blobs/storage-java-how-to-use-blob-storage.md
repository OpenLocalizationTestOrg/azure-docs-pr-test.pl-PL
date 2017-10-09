---
title: "toouse aaaHow magazynu obiektów Blob platformy Azure (obiekt magazynu) w języku Java | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
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
ms.openlocfilehash: a905d318abdaa7538ec3f6b53b5186b965b8b86e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Jak toouse magazynu obiektów Blob w języku Java
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Omówienie
Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

W tym artykule opisano sposób tooperform typowych scenariuszy przy użyciu hello magazynu obiektów Blob Microsoft Azure. Hello przykłady są napisane w języku Java i używają hello [Azure Storage SDK for Java][Azure Storage SDK for Java]. Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob. Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz hello [następne kroki](#Next-Steps) sekcji.

> [!NOTE]
> Zestaw SDK jest dostępny dla deweloperów, którzy korzystają z usługi Azure Storage na urządzeniach z systemem Android. Aby uzyskać więcej informacji, zobacz hello [zestawu SDK usługi Magazyn Azure dla systemu Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Tworzenie aplikacji Java
W tym artykule użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji Java lokalnie lub w kodzie działających w roli sieci web lub roli proces roboczy na platformie Azure.

toodo tak, konieczne będzie tooinstall hello Java Development Kit (JDK) i utworzyć konto magazynu Azure w ramach subskrypcji platformy Azure. Po zostało to zrobione, należy tooverify spełniającym w systemie deweloperskim hello minimalne wymagania i zależności, które są wymienione w hello [Azure Storage SDK for Java] [ Azure Storage SDK for Java] repozytorium w witrynie GitHub. Jeżeli komputer spełnia te wymagania, należy wykonać hello instrukcje dotyczące pobierania i instalowania hello biblioteki magazynu Azure dla języka Java w systemie z tego repozytorium. Po wykonaniu tych zadań, będzie możliwe toocreate aplikacji Java, który używa hello przykłady w tym artykule.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu obiektów Blob
Dodaj powitania od góry toohello instrukcje importu hello Java pliku którego toouse hello interfejsy API usługi Azure Storage tooaccess blob.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Konfigurowanie parametrów połączenia magazynu Azure
Klienta usługi Azure Storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, przy użyciu hello nazwy konta magazynu i hello podstawowy klucz dostępu dla konta magazynu hello na liście hello [portalu Azure](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości. Witaj poniższy przykład przedstawia sposób można zadeklarować ciąg połączenia hello toohold pola statycznego.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

W aplikacji działającej w ramach roli w systemie Microsoft Azure, te parametry mogą być przechowywane w pliku konfiguracji usługi hello, *pliku ServiceConfiguration.cscfg*i jest dostępny z toohello wywołania  **RoleEnvironment.getConfigurationSettings** metody. Witaj poniższy przykład pobiera parametry połączenia hello z **ustawienie** elementu o nazwie *StorageConnectionString* w pliku konfiguracji usługi hello.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.

## <a name="create-a-container"></a>Tworzenie kontenera
A **CloudBlobClient** obiektu pozwala pobierać obiekty odwołań dla kontenerów i obiektów blob. Witaj poniższy kod tworzy **CloudBlobClient** obiektu.

> [!NOTE]
> Istnieją dodatkowe sposoby toocreate **CloudStorageAccount** obiektów; Aby uzyskać więcej informacji, zobacz **CloudStorageAccount** w hello [odwołania do zestawu SDK klienta magazynu Azure].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Użyj hello **CloudBlobClient** tooget kontener toohello odwołanie ma toouse obiektu. Można utworzyć kontenera hello, jeśli nie istnieje z hello **createIfNotExists** metody, które w przeciwnym razie zwraca hello istniejącego kontenera. Domyślnie nowy kontener hello jest prywatny, więc (tak samo jak wcześniej), należy określić klucz dostępu do magazynu obiektów blob toodownload z tego kontenera.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Opcjonalnie: Konfigurowanie kontener dla dostępu publicznego
Kontener uprawnienia są domyślnie skonfigurowane dla dostępu prywatnego, ale można łatwo skonfigurować kontenera uprawnienia tooallow publiczne, tylko do odczytu dostęp dla wszystkich użytkowników na powitania Internet:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
tooupload obiektu blob tooa plik, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob. Po utworzeniu odwołanie do obiektu blob, możesz przekazać strumieniem, wywołując przekazywania hello w odwołaniu do obiektu blob. Ta operacja spowoduje utworzenie obiektu blob hello, jeśli nie istnieje lub jego zastąpienie, jeśli istnieje. powitania po przykładowy kod przedstawia to przyjęto założenie, że kontenera hello został już utworzony.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
jak tooupload obiektu blob toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera. Korzystając z kontenera hello **listBlobs** metody z **dla** pętli. Witaj poniższy kod wyświetla hello Uri każdy obiekt blob w kontenerze toohello konsoli.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Należy pamiętać, nazwę obiekty BLOB zawierające informacje o ścieżce ich nazw. Powoduje to utworzenie wirtualnej struktury katalogów, które można organizować i przechodzić między nimi tak jak w przypadku tradycyjnego systemu plików. Należy pamiętać, że struktura katalogów hello jest wyłącznie wirtualna — hello tylko zasoby dostępne w magazynie obiektów Blob to kontenery i obiekty BLOB. Jednak biblioteka klienta hello oferuje **CloudBlobDirectory** obiektu katalogu wirtualnego tooa toorefer i uprościć proces hello Praca z obiektami blob zorganizowanymi w ten sposób.

Na przykład można mieć kontener o nazwie "zdjęć", w których może przekazać obiekty BLOB o nazwie "rootphoto1", "2010/photo1", "2010/photo2" i "2011/photo1". Spowoduje to utworzenie hello katalogi wirtualne "2010" i "2011" w kontenerze "zdjęć" hello. Podczas wywoływania **listBlobs** w kontenerze "zdjęć" hello, będzie zawierać hello kolekcji zwróconej **CloudBlobDirectory** i **CloudBlob** obiekty reprezentujące hello katalogi i obiekty BLOB zawarte na najwyższym poziomie hello. W takim przypadku katalogi "2010" i "2011", a także photo "rootphoto1" zostałaby zwrócona. Można użyć hello **instanceof** operator toodistinguish tych obiektów.

Opcjonalnie można przekazać parametry toohello **listBlobs** metody z hello **useFlatBlobListing** tootrue ustawiony parametr. Spowoduje to każdy obiekt blob zostały zwrócone, niezależnie od tego katalogu. Aby uzyskać więcej informacji, zobacz **CloudBlobContainer.listBlobs** w hello [odwołania do zestawu SDK klienta magazynu Azure].

## <a name="download-a-blob"></a>Pobieranie obiektu blob
toodownload obiektów blob, wykonaj kroki takie same jak dla obiektu blob w kolejności tooget odwołanie do obiektu blob wysyłanie hello. W hello przekazywania przykład przekazywanie wywołano hello obiektu blob. W hello poniższy przykład, należy wywołać pobierania tootransfer hello blob zawartość tooa strumienia obiektu takich jak **FileOutputStream** służy pliku lokalnego tooa toopersist hello obiektu blob.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Usuwanie obiektu blob
toodelete obiektu blob, Pobierz obiekt blob odwołania i Wywołaj **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Usunięcie kontenera obiektów blob
Na koniec toodelete kontenera obiektów blob, Pobierz obiekt blob odwołanie do kontenera i wywołanie **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu obiektów Blob hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* [Magazyn Azure SDK dla języka Java][Azure Storage SDK for Java]
* [Odwołanie do zestawu SDK klienta usługi Azure Storage][odwołania do zestawu SDK klienta magazynu Azure]
* [Interfejs API REST usługi Azure Storage][Azure Storage REST API]
* [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog]

Aby uzyskać więcej informacji, zobacz też [Azure dla deweloperów języka Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[odwołania do zestawu SDK klienta magazynu Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
