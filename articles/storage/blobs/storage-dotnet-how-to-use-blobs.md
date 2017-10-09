---
title: "aaaGet pracy z magazynem obiektów Blob platformy Azure (obiekt magazynu), przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

### <a name="about-this-tutorial"></a>Informacje o tym samouczku
Ten samouczek pokazuje, jak kod toowrite .NET dla niektórych typowych scenariuszy przy użyciu magazynu obiektów Blob platformy Azure. Przedstawione scenariusze obejmują przekazywanie, pobieranie i usuwanie obiektów blob oraz wyświetlanie ich listy.

**Wymagania wstępne:**

* [Program Microsoft Visual Studio](https://www.visualstudio.com/)
* [Biblioteka klienta usługi Azure Storage dla programu .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Menedżer konfiguracji Azure dla programu .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [konto usługi Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Więcej przykładów
Dodatkowe przykłady użycia usługi Blob Storage znajdziesz w temacie [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Rozpoczynanie pracy z usługą Azure Blob Storage w programie .NET). Możesz pobrać hello przykładowej aplikacji i uruchom go lub Przeglądaj hello kodu w witrynie GitHub.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Dodawanie dyrektyw using
Dodaj następujące hello **przy użyciu** dyrektywy toohello początku hello `Program.cs` pliku:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Przeanalizować parametrów połączenia hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Tworzenie klienta usługi Blob hello
Witaj **CloudBlobClient** klasy pozwala tooretrieve kontenery i obiekty BLOB przechowywane w magazynie obiektów Blob. Klient usługi jednokierunkowej toocreate hello jest następujący:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Teraz wszystko jest gotowe toowrite kod odczytuje i zapisuje tooBlob pamięci masowej.

## <a name="create-a-container"></a>Tworzenie kontenera
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

W tym przykładzie pokazano sposób toocreate kontenera, jeśli jeszcze nie istnieje:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Domyślnie program hello nowy kontener jest prywatny, co oznacza, że obiektów blob toodownload klucza dostępu do magazynu z tego kontenera należy określić. Jeśli chcesz, aby pliki hello toomake tooeveryone dostępne kontenera hello, można ustawić toobe kontenera hello publiczny przy użyciu następującego kodu hello:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym. Jednak można zmodyfikować lub usunąć je tylko wtedy, gdy masz hello odpowiednie konto dostępu do klucza lub sygnatury dostępu współdzielonego.

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob.  W większości przypadków blokowych obiektów blob jest hello zalecane toouse typu.

tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku. Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **UploadFromStream** metody. Ta operacja tworzy hello obiektów blob, jeśli wcześniej nie istnieje lub zastąpiony, jeśli istnieje.

powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera. Można użyć kontenera hello **ListBlobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi. bogaty zestaw właściwości i metod zwróconego hello tooaccess **IListBlobItem**, należy rzutować go tooa **CloudBlockBlob**, **CloudPageBlob**, lub  **CloudBlobDirectory** obiektu. Jeśli typ hello jest nieznany, można użyć toodetermine wyboru typu które toocast jej. Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello _zdjęć_ kontenera:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

Uwzględniając informacje o ścieżce w nazwach obiektów blob, można utworzyć wirtualną strukturę katalogów, które można organizować i przechodzić między nimi tak jak w przypadku tradycyjnego systemu plików. Struktura katalogów Hello jest wirtualna tylko — Witaj tylko zasoby dostępne w magazynie obiektów Blob to kontenery i obiekty BLOB. Jednak biblioteka klienta magazynu hello zapewnia **CloudBlobDirectory** obiektu katalogu wirtualnego tooa toorefer i uprościć proces hello Praca z obiektami blob zorganizowanymi w ten sposób.

Na przykład, należy wziąć pod uwagę następujące zestaw blokowych obiektów blob w kontenerze o nazwie hello *zdjęć*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Podczas wywoływania **ListBlobs** na powitania *zdjęć* kontenera (jak hello poprzedzających fragment kodu), zwrócenie listy hierarchicznej. Zawiera **CloudBlobDirectory** i **CloudBlockBlob** obiekty reprezentujące odpowiednio hello katalogi i obiekty BLOB w kontenerze hello. Witaj dane wyjściowe wyglądają następująco:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Opcjonalnie można ustawić hello **UseFlatBlobListing** parametru hello **ListBlobs** metodę **true**. W takim przypadku każdy obiekt blob w kontenerze hello jest zwracana jako **CloudBlockBlob** obiektu. Witaj wywołanie za**ListBlobs** tooreturn listy niezhierarchizowanej wygląda następująco:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

i hello wyniki wyglądają następująco:

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Pobieranie obiektów blob
obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **DownloadToStream** metody. Witaj poniższym przykładzie użyto hello **DownloadToStream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

Można również użyć hello **DownloadToStream** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Usuwanie obiektów blob
toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać **usunąć** dla niego metodę.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Asynchroniczne wyświetlanie obiektów blob na stronach
Jeśli chcesz wyświetlić dużą liczbę obiektów blob lub ma toocontrol hello liczbę wyników zwracanych przez jedną operację wyświetlania listy, można wyświetlić listę obiektów blob na stronach wyników. Ten przykład przedstawia, jak tooreturn wyników na stronach asynchronicznie, dzięki czemu wykonanie nie jest blokowane podczas oczekiwania tooreturn dużych zestawów wyników.

W tym przykładzie przedstawiono niezhierarchizowaną listę obiektów blob, ale można również wykonywać listę hierarchiczną, przez ustawienie hello _useFlatBlobListing_ parametru hello **ListBlobsSegmentedAsync** too_false_ metody.

Ponieważ hello przykładowa metoda wywołuje metodę asynchroniczną, musi być poprzedzona słowem hello _async_ — słowo kluczowe, a musi zwracać **zadań** obiektu. określona dla hello — słowo kluczowe await Hello **ListBlobsSegmentedAsync** wstrzymuje wykonywanie hello przykładowej metody do momentu ukończenia zadania wyświetlania listy hello.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a>Zapisywanie tooan Dołącz obiektów blob
Uzupełnialny obiekt blob jest zoptymalizowany pod kątem operacji dołączania, takich jak rejestrowanie. Podobnie jak blokowy obiekt blob uzupełnialny obiekt blob jest złożony z bloków, ale po dodaniu nowego bloku tooan uzupełnialny obiekt blob jest zawsze toohello dołączany na końcu obiektu blob hello. Nie można zaktualizować lub usunąć istniejącego bloku w uzupełnialnym obiekcie blob. Witaj identyfikatory bloków w uzupełnialnym obiekcie blob nie są widoczne, jak w przypadku blokowego obiektu blob.

Każdy blok w uzupełnialnym obiekcie blob może być inny rozmiar się tooa maksymalnie 4 MB, a uzupełnialny obiekt blob może zawierać maksymalnie 50 000 bloków. Maksymalny rozmiar uzupełnialnego obiektu blob Hello w związku z tym jest nieco przekraczać 195 GB (4 MB X 50 000 bloków).

w poniższym przykładzie Hello tworzy nowy uzupełnialny obiekt blob i dołącza tooit niektóre dane, symulując prostą operację rejestrowania.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Zobacz [opis blokowe, stronicowe obiekty BLOB i Dołącz obiektów blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) Aby uzyskać więcej informacji o różnicach hello hello trzy typy obiektów blob.

## <a name="managing-security-for-blobs"></a>Zarządzanie zabezpieczeniami obiektów blob
Domyślnie usługi Azure Storage chroni dane, ograniczając toohello właściciela konta dostępu, który znajduje się w posiadaniu klucze dostępu do konta hello. Jeśli potrzebujesz tooshare danych obiektów blob na koncie magazynu jest ważne toodo tak bez naruszania zabezpieczeń hello kluczy dostępu do konta. Ponadto można zaszyfrować tooensure danych obiektów blob, który jest bezpieczne, przejdź na powitania przewodowy i w usłudze Azure Storage.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Kontrolowanie dostępu do danych tooblob
Domyślnie program hello danych obiektów blob na koncie magazynu jest dostępny tylko właściciel konta toostorage. Uwierzytelniania żądań dotyczących magazynu obiektów Blob wymaga klucz dostępu do konta hello domyślnie. Jednak możesz toomake niektórych użytkowników tooother dostępnych danych obiektu blob. Dostępne są dwie opcje:

* **Dostęp anonimowy:** możesz ustawić kontener lub zawarte w nim obiekty blob jako dostępne publicznie, aby umożliwić dostęp anonimowy. Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](storage-manage-access-to-resources.md) Aby uzyskać więcej informacji.
* **Sygnatury dostępu współdzielonego:** możesz zapewnić klientom sygnatury dostępu współdzielonego (SAS), która zapewnia dostęp delegowany tooa zasobów na koncie magazynu z uprawnieniami, które określisz i interwału, który określisz. Zobacz [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji.

### <a name="encrypting-blob-data"></a>Szyfrowanie danych obiektów blob
Usługa Azure Storage obsługuje szyfrowanie danych obiektów blob, zarówno na powitania klienta, jak i na serwerze hello:

* **Szyfrowanie po stronie klienta:** hello biblioteki klienta usługi Storage dla platformy .NET obsługuje szyfrowania danych w aplikacjach klienckich przed przekazaniem tooAzure magazynu i odszyfrowywania danych podczas pobierania toohello klienta. Biblioteka Hello obsługuje również integrację z usługą Azure Key Vault do zarządzania kluczami konta magazynu. Aby uzyskać więcej informacji, zobacz [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Szyfrowanie po stronie klienta przy użyciu programu .NET dla usługi Microsoft Azure Storage). Zobacz również [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md) (Samouczek: szyfrowanie i odszyfrowywanie obiektów blob w usłudze Microsoft Azure Storage przy użyciu usługi Azure Key Vault).
* **Szyfrowanie po stronie serwera**: usługa Azure Storage obsługuje teraz szyfrowanie po stronie serwera. Zobacz [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Szyfrowanie usługi Azure Storage dla danych magazynowanych (wersja zapoznawcza)).

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu obiektów Blob hello, wykonaj te więcej toolearn łącza.

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Explorer
* [Microsoft Azure magazynu Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.

### <a name="blob-storage-samples"></a>Przykłady użycia usługi Blob Storage
* [Rozpoczynanie pracy z usługą Azure Blob Storage na platformie .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Informacje o usłudze Blob Storage
* [Dokumentacja biblioteki klienta usługi Storage dla programu .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Dokumentacja interfejsu API REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Przewodniki koncepcyjne
* [Transfer danych za pomocą hello wiersza polecenia azcopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Wprowadzenie do usługi File Storage dla platformy .NET](../files/storage-dotnet-how-to-use-files.md)
* [Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
