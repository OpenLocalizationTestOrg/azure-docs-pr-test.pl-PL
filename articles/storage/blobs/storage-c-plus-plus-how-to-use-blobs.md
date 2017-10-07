---
title: aaaHow toouse obiektu blob magazynu (obiekt) z C++ | Dokumentacja firmy Microsoft
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Jak toouse magazynu obiektów Blob w języku C++
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

W tym przewodniku przedstawiono sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu obiektów Blob platformy Azure. Hello przykłady są napisane w języku C++ i używają hello [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Witaj omówione scenariusze obejmują **przekazywania**, **wyświetlania**, **pobieranie**, i **usuwanie** obiektów blob.  

> [!NOTE]
> Cele tego przewodnika hello biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej. Hello zalecana jest wersja biblioteki klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Tworzenie aplikacji C++
W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.  

toodo tak, konieczne będzie tooinstall hello biblioteki klienta magazynu Azure dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.   

Witaj tooinstall biblioteki klienta magazynu Azure dla języka C++, można użyć hello następujące metody:

* **Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.  
* **System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**. Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.  
  
     Pakiet instalacyjny wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu obiektów Blob
Dodaj wlicza się hello następujące instrukcje toohello górnej części pliku C++ hello miejscu obiekty BLOB tooaccess interfejsów API toouse hello magazynu Azure:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Konfiguracja parametrów połączenia usługi Azure storage
Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, używając hello nazwę konta i hello magazynu klucz dostępu do magazynu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości. Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest aplikacji w lokalnym komputerze z systemem Windows, można użyć hello Microsoft Azure [emulatora magazynu](../storage-use-emulator.md) zainstalowane z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/). emulator magazynu Hello jest narzędziem, która symuluje hello dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli. Witaj poniższym przykładzie pokazano, jak można zadeklarować pola statycznego toohold hello połączenia ciąg tooyour lokalnym emulatorze magazynu:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulatora magazynu Azure hello toostart, wybierz opcję hello **Start** hello przycisk lub naciśnij przycisk **Windows** klucza. Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z hello listy aplikacji.  

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.  

## <a name="retrieve-your-connection-string"></a>Pobranie parametrów połączenia
Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu. tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Następnie Pobierz tooa odwołanie **cloud_blob_client** klasa umożliwia tooretrieve obiektów, które reprezentują kontenery i obiekty BLOB przechowywane w ramach hello usługi magazynu obiektów Blob. Witaj poniższy kod tworzy **cloud_blob_client** obiektu przy użyciu obiektu konta magazynu hello możemy pobrać powyżej:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Porady: Tworzenie kontenera
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

W tym przykładzie pokazano sposób toocreate kontenera, jeśli jeszcze nie istnieje:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Domyślnie nowy kontener hello jest prywatny i należy określić obiektów blob toodownload klucza dostępu do magazynu z tego kontenera. Jeśli chcesz toomake hello plików (BLOB) w ramach tooeveryone dostępne kontenera hello toobe kontenera hello można ustawić publiczny przy użyciu następującego kodu hello:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Wszyscy użytkownicy hello Internetu mogą wyświetlać obiekty BLOB w kontenerze publicznym, ale można zmodyfikować lub usunąć je tylko wtedy, gdy klucz dostępu odpowiednie hello.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Porady: przekazywanie obiektu blob do kontenera
Azure Blob Storage obsługuje blokowe i stronicowe obiekty blob. W większości przypadków hello blokowych obiektów blob jest hello zalecane toouse typu.  

tooupload pliku tooa blokowego obiektu blob, Pobierz odwołanie do kontenera i korzystać z niego tooget odwołanie do obiektu blob bloku. Po utworzeniu odwołanie do obiektu blob możesz przekazać dowolny strumień danych tooit przez wywołanie hello **upload_from_stream** metody. Ta operacja spowoduje utworzenie obiektu blob hello, jeśli on nie istnieje, lub go zastąpić, jeśli istnieje. powitania po przykładzie pokazano, jak tooupload obiektu blob do kontenera i zakłada kontenera hello został już utworzony.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Alternatywnie można użyć hello **upload_from_file** tooupload metody tooa pliku blokowego obiektu blob.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Porady: wyświetlanie obiektów blob hello w kontenerze
toolist hello BLOB w kontenerze, najpierw pobrać odwołanie do kontenera. Można użyć kontenera hello **list_blobs** obiekty BLOB hello tooretrieve — metoda i/lub zawarte w nim katalogi. tooaccess hello bogatego zestawu właściwości i metod zwróconego **list_blob_item**, należy wywołać hello **list_blob_item.as_blob** tooget metody **cloud_blob** obiektu lub hello **list_blob.as_directory** tooget metody obiektu cloud_blob_directory. Witaj poniższy kod przedstawia sposób tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w hello **Moje kontenera próbki** kontenera:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Więcej szczegółów na listę działań, zobacz [listy zasobów magazynu Azure w języku C++](../storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Porady: pobieranie obiektów blob
obiekty BLOB toodownload, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **download_to_stream** metody. Witaj poniższym przykładzie użyto hello **download_to_stream** metody tootransfer hello blob zawartość tooa obiektu strumienia można następnie zachować tooa pliku lokalnego.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Alternatywnie można użyć hello **download_to_file** metody toodownload hello zawartości pliku tooa obiektu blob.
Ponadto można również użyć hello **download_text** metody toodownload hello zawartość obiektu blob jako ciąg tekstowy.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Porady: usuwanie obiektów blob
toodelete obiektu blob, najpierw pobrać odwołanie do obiektu blob, a następnie wywołać hello **delete_blob** dla niego metodę.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu obiektów blob hello, wykonaj te toolearn łącza więcej informacji na temat usługi Azure Storage.  

* [Jak toouse magazynu kolejek w języku C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Jak toouse magazynu tabel w języku C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Lista zasobów magazynu Azure w języku C++](../storage-c-plus-plus-enumeration.md)
* [Biblioteka klienta usługi Storage for C++ — dokumentacja](http://azure.github.io/azure-storage-cpp)
* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Transfer danych za pomocą hello wiersza polecenia azcopy](../storage-use-azcopy.md)

