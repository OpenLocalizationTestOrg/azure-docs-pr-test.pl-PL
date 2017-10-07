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
# <a name="develop-for-azure-file-storage-with-java"></a>Tworzenie dla usługi Magazyn plików Azure z językiem Java
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Informacje o tym samouczku
W tym samouczku przedstawiono podstawy hello za pomocą języka Java toodevelop aplikacje lub usługi, które używają danych pliku toostore magazyn plików Azure. W tym samouczku utworzymy prostej aplikacji konsolowej ją i Pokaż jak podstawowe czynności tooperform z magazynem Java i plików platformy Azure:

* Tworzenie i usuwanie udziałów plików Azure
* Tworzenie i usuwanie katalogów
* Wyliczanie plików i katalogów w udziale plików Azure
* Przekazywanie, pobieranie i usuwanie pliku

> [!Note]  
> Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików platformy Azure hello przy użyciu standardowych klas Java we/wy hello. W tym artykule opisano, jak toowrite aplikacji, które używają hello SDK Java magazynu Azure, która używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.

## <a name="create-a-java-application"></a>Tworzenie aplikacji Java
Przykłady hello toobuild, konieczne będzie hello Java Development Kit (JDK) i hello [Azure Storage SDK for Java] []. Należy również utworzono konto magazynu platformy Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Instalator programu toouse aplikacji usługi Magazyn plików Azure
Witaj toouse magazynu Azure interfejsów API, Dodaj powitania po instrukcji toohello górnej części pliku Java hello, w którym ma tooaccess hello magazynu usługi z.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Konfiguracja parametrów połączenia usługi Azure storage
toouse magazyn plików Azure, musisz mieć konto magazynu Azure tooyour tooconnect. Witaj pierwszym krokiem będzie tooconfigure parametry połączenia, które będą używane konto magazynu tooyour tooconnect. Umożliwia definiowanie statycznego toodo zmiennej który.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Zamień your_storage_account_name i your_storage_account_key hello rzeczywiste wartości dla konta magazynu.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Łączenie z kontem magazynu platformy Azure tooan
tooconnect tooyour konta magazynu, należy toouse hello **CloudStorageAccount** przekazania tooits ciąg połączenia obiektu **przeanalizować** metody.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** zwraca InvalidKeyException, dlatego potrzebujesz tooput zablokować go w programie try/catch.

## <a name="create-an-azure-file-share"></a>Tworzenie udziału plików platformy Azure
Wszystkich plików i katalogów w usłudze magazyn plików Azure znajdują się w kontenerze o nazwie **udziału**. Twoje konto magazynu może mieć tyle udziałów zezwala pojemności Twojego konta. tooobtain dostępu tooa udziału i jego zawartość, należy toouse klienta magazyn plików Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Za pomocą klienta magazyn plików Azure hello można następnie uzyskać udziału tooa odwołania.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually utworzyć udział hello, użyj hello **createIfNotExists** metody hello CloudFileShare obiektu.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

W tym momencie **udostępnianie** posiada udział tooa odwołania o nazwie **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Usuń udział plików Azure
Usuwanie udziału jest realizowane przez wywołanie hello **deleteIfExists** metody dla obiekt CloudFileShare. Oto przykładowy kod, który robi to.

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

## <a name="create-a-directory"></a>Tworzenie katalogu
Możesz również dzielić magazynu przez umieszczenie plików wewnątrz podkatalogów zamiast wszystkich z nich w katalogu głównym hello. Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów, jako Twoje konto zostanie. Poniższy kod Hello utworzy podkatalogu o nazwie **sampledir** w katalogu głównym hello.

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

## <a name="delete-a-directory"></a>Usuwanie katalogu
Usunięcie katalogu jest dość proste zadania, jednak należy zauważyć, że nie można usunąć katalogu, w którym nadal zawiera pliki lub katalogi innych.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Wyliczanie plików i katalogów w udziale plików Azure
Uzyskiwanie listy plików i katalogów w udziale łatwo odbywa się przez wywołanie metody **listFilesAndDirectories** na odwołanie CloudFileDirectory. Metoda Hello zwraca listę ListFileItem obiektów, które można wykonać iterację na. Na przykład hello następujący kod będzie zawierała listę plików i katalogów w katalogu głównym hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Przekazywanie pliku
Plik Azure, który zawiera na powitania bardzo najmniej udziału, katalog główny, w którym mogą znajdować się pliki. W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.

pierwszym krokiem Hello przekazywania pliku jest tooobtain katalogu toohello odwołania, gdzie powinien znajdować się. W tym celu wywoływania hello **getRootDirectoryReference** metody hello udziału obiektu.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Teraz, gdy masz katalog główny odwołania toohello hello udziału, możesz przekazać plik na przy użyciu następującego kodu hello.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Pobieranie pliku
Jednym z hello częstsze operacje, które będą wykonywane względem usługi Magazyn plików Azure jest toodownload plików. W hello poniższy przykład hello kod pobiera SampleFile.txt i wyświetla jego zawartość.

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

## <a name="delete-a-file"></a>Usuwanie pliku
Inna operacja magazynu plików Azure wspólnej jest usuwanie plików. Witaj następujący kod usuwa plik o nazwie SampleFile.txt przechowywany w katalogu o nazwie **sampledir**.

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

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz toolearn więcej informacji na temat innych interfejsów API magazynu Azure, skorzystaj z poniższych linków.

* [Azure dla deweloperów języka Java](/java/azure)/)
* [Magazyn Azure SDK dla języka Java](https://github.com/azure/azure-storage-java)
* [Magazyn Azure SDK dla systemu Android](https://github.com/azure/azure-storage-android)
* [Odwołanie do zestawu SDK klienta usługi Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)