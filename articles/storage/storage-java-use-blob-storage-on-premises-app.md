---
title: "aaaOn lokalnych aplikacji z magazynem obiektów blob (w języku Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikacja konsolowa, która przekazuje tooAzure obrazu, a następnie wyświetla hello obraz w przeglądarce. Przykłady kodu w języku Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Aplikacji lokalnych przy użyciu magazynu obiektów blob
## <a name="overview"></a>Omówienie
Hello poniższym przykładzie pokazano sposób korzystania magazynu Azure do przechowywania obrazów na platformie Azure. Kod Hello w tym artykule jest dla aplikacji konsoli, która przekazuje tooAzure obrazu, a następnie tworzy plik HTML, który wyświetla obraz powitania w przeglądarce.

## <a name="prerequisites"></a>Wymagania wstępne
* Java Developer Kit (JDK), w wersji 1.6 lub nowszej, jest zainstalowana.
* Witaj zestawu Azure SDK jest zainstalowany.
* Hello JAR hello Azure bibliotek języka Java i wszelkie słoików odpowiednich zależności są zainstalowane i są w ścieżce kompilacji hello używany przez Twoje kompilator języka Java. Informacje o instalowaniu hello biblioteki Azure dla języka Java, zobacz [hello Pobierz zestaw Azure SDK for Java](../java-download-azure-sdk.md).
* Konto magazynu platformy Azure został skonfigurowany. Witaj nazwę konta i klucz konta usługi dla konta magazynu hello będą korzystali hello kodu w tym artykule. Zobacz [jak tooCreate konta magazynu](storage-create-storage-account.md#create-a-storage-account) informacji o tworzeniu konta magazynu i [wyświetlanie i kopiowanie kluczy dostępu do magazynu](storage-create-storage-account.md#view-and-copy-storage-access-keys) informacje o pobieraniu hello klucz konta.
* Utworzono plik obrazu lokalnego o nazwie przechowywanych na powitania ścieżka c:\\myimages\\image1.jpg. Można również zmodyfikować **FileInputStream** konstruktora w toouse przykład hello ścieżkę i nazwę innego obrazu.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload magazynu obiektów blob platformy Azure toouse pliku
W tym miejscu przedstawiono procedury krok po kroku. Jeśli chcesz tooskip wyprzedzeniem hello całego kodu przedstawiono w dalszej części tego artykułu.

Rozpocząć hello kodu przy tym Importy dla klasy magazynu Azure core hello, klasy klienta obiektów blob platformy Azure hello hello klasy Java We/Wy i hello **URISyntaxException** klasy.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Deklarowanie klasy o nazwie **StorageSample**i zawierają hello otwierającego nawiasu **{**.

```java
public class StorageSample {
```

W ramach hello **StorageSample** klasy, zadeklarować zmiennej ciągu, która będzie zawierała hello domyślnego punktu końcowego protokołu, nazwa konta magazynu i klucz dostępu do magazynu, zgodnie z kontem magazynu platformy Azure. Zastąp symbole zastępcze hello **Twojego\_konta\_nazwa** i **Twojego\_konta\_klucza** z własną nazwę konta i klucz konta odpowiednio.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Dodaj w deklaracji pod kątem **głównego**, obejmują **spróbuj** zablokować, a także zawierać hello niezbędne otwartych nawiasów, **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Deklarowanie zmiennych hello następującego typu (powitalne opisy są do korzystania z nich w tym przykładzie):

* **CloudStorageAccount**: hello tooinitialize używane konto obiektu z nazwy konta magazynu Azure, a klucz i toocreate obiektu blob klienta.
* **CloudBlobClient**: używana usługa blob hello tooaccess.
* **CloudBlobContainer**: używane toocreate kontenera obiektów blob, listę obiektów blob w kontenerach hello i usuwania hello kontenera.
* **CloudBlockBlob**: tooupload używane kontener toothe pliku obrazu lokalnego.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Przypisz toohello wartość **konta** zmiennej.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Przypisz toohello wartość **serviceClient** zmiennej.

```java
serviceClient = account.createCloudBlobClient();
```

Przypisz toohello wartość **kontenera** zmiennej. Możemy uzyskać tooa odwołanie do kontenera o nazwie **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Tworzenie kontenera hello. Ta metoda utworzy kontener hello, jeśli nie istnieje (i zwracać **true**). Jeśli istnieje hello kontenera, będzie zwracać **false**. Zamiast zbyt**createIfNotExists** jest hello **utworzyć** — metoda (co spowoduje zwrócenie błędu, jeśli hello kontener już istnieje).

```java
container.createIfNotExists();
```

Ustaw dostęp anonimowy hello kontenera.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Pobierz odwołanie toohello blokowego obiektu blob, który będzie reprezentował hello blob w magazynie Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Użyj hello **pliku** tooget konstruktora, który trzeba będzie przekazać pliku toohello utworzony lokalnie odwołań. Upewnij się, że ten plik został utworzony przed uruchomieniem kodu hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Przekaż hello pliku lokalnego za pomocą toohello wywołania **CloudBlockBlob.upload** metody. Witaj pierwszy parametr toohello **CloudBlockBlob.upload** jest metoda **FileInputStream** obiekt tego reprezentuje hello lokalnego pliku, który ma być przekazany tooAzure magazynu. drugi parametr Hello jest hello wyrażony w bajtach rozmiar, hello pliku.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Wywoływanie funkcji pomocnika o nazwie **MakeHTMLPage**, toomake podstawowe HTML strony, która zawiera  **&lt;obrazu&gt;**  element z hello źródła zestawu toohello blob, który znajduje się teraz w platformy Azure Konto magazynu. Witaj kod **MakeHTMLPage** zostanie dokładnie omówione w dalszej części tego artykułu.

```java
MakeHTMLPage(container);
```

Drukowanie komunikatów o stanie i informacje o hello utworzona strona HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Zamknij hello **spróbuj** bloku wstawiając nawiasu zamykającego: **}**

Obsługa hello następujące wyjątki:

* **FileNotFoundException**: może zostać wygenerowany przez hello **FileInputStream** lub **FileOutputStream** konstruktorów.
* **StorageException**: może zostać wygenerowany przez biblioteki usługi powitania klienta usługi Azure storage.
* **URISyntaxException**: może zostać wygenerowany przez hello **ListBlobItem.getUri** metody.
* **Wyjątek**: obsługa wyjątków ogólnych.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Zamknij **głównego** wstawiając nawiasu zamykającego: **}**

Utwórz metodę o nazwie **MakeHTMLPage** toocreate podstawowe HTML strony. Ta metoda ma parametr typu **CloudBlobContainer**, które będzie używane tooiterate za pośrednictwem listy hello przekazane obiektów blob. Ta metoda zgłosi wyjątki typu **FileNotFoundException**, który może zostać wygenerowany przez hello **FileOutputStream** konstruktora, i **URISyntaxException**, co może być zgłaszany przez hello **ListBlobItem.getUri** metody. Obejmować nawias otwierający **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Tworzenie pliku lokalnego o nazwie **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Zapis pliku lokalnego toohello, dodanie hello  **&lt;html&gt;**,  **&lt;nagłówka&gt;**, i  **&lt;treści&gt;**  elementów.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Iterowanie za pomocą listy hello przekazane obiektów blob. Dla każdego obiektu blob, na stronie powitania HTML utworzyć  **&lt;img&gt;**  element, który ma jego **src** atrybut wysłany do hello identyfikator URI obiektu hello blob, ponieważ znajduje się na koncie magazynu Azure.
Mimo że tylko jeden obraz został dodany w tym przykładzie, jeśli został dodany więcej, ten kod będzie Iterowanie wszystkich z nich.

Dla uproszczenia w tym przykładzie przyjęto założenie, że każdy przekazany obiekt blob jest obrazem. Jeśli użytkownik zaktualizował obiektów blob innego niż obrazy lub stronicowe obiekty BLOB zamiast blokowych obiektów blob, Dostosuj kod hello zgodnie z potrzebami.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Zamknij hello  **&lt;treści&gt;**  elementu i hello  **&lt;html&gt;**  elementu.

```java
stream.println("</body>");
stream.println("</html>");
```

Zamknij hello pliku lokalnego.

```java
stream.close();
```

Zamknij **MakeHTMLPage** wstawiając nawiasu zamykającego: **}**

Zamknij **StorageSample** wstawiając nawiasu zamykającego: **}**

Oto Hello hello kompletny kod dla tego przykładu. Pamiętaj symbole zastępcze hello toomodify **Twojego\_konta\_nazwa** i **Twojego\_konta\_klucza** toouse nazwę konta i konta klucz, odpowiednio.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

W toouploading dodanie obrazu lokalnego pliku magazynu tooAzure, hello przykładowy kod tworzy namedindex.html pliku lokalnego, który można otworzyć w Twojej przeglądarce toosee Twojego załadowanego obrazu.

Ponieważ kod hello zawiera nazwę konta i klucz konta usługi, upewnij się, że kod źródłowy jest bezpieczna.

## <a name="toodelete-a-container"></a>toodelete kontenera
Ponieważ naliczane są opłaty za magazyn, może być toodelete **gettingstarted** kontenera po zakończeniu eksperymentowanie z tego przykładu. toodelete kontener, użyj hello **CloudBlobContainer.delete** metody.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Witaj toocall **CloudBlobContainer.delete** metoda, proces inicjowania hello **CloudStorageAccount**, **ClodBlobClient**, i  **CloudBlobContainer** obiektów jest taki sam, jak pokazano na hello **createIfNotExist** metody. Witaj poniżej znajduje się pełny przykład, że usuwa hello kontener o nazwie **gettingstarted**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Omówienie inne klasy magazynu obiektów blob i metody, zobacz [jak toouse magazynu obiektów Blob w języku Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Następne kroki
Wykonaj te toolearn łącza więcej o bardziej skomplikowanych zadaniach magazynu.

* [Magazyn Azure SDK dla języka Java](https://github.com/azure/azure-storage-java)
* [Odwołanie do zestawu SDK klienta usługi Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

