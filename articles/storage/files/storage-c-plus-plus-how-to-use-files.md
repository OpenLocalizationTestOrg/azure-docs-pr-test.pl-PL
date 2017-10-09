---
title: aaaDevelop Azure File Storage z C++ | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dane plików toodevelop C++ aplikacji i usług, które używają toostore magazyn plików Azure."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Tworzenie dla usługi Magazyn plików Azure z C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Informacje o tym samouczku

W przypadku tego samouczka, dowiesz się, jak tooperform podstawowe operacje na magazyn plików Azure. Za pomocą przykłady w języku C++, dowiesz się, jak toocreate udziałów i katalogi, przekazywanie, listy i Usuń pliki. W przypadku nowego magazynu plików tooAzure pośrednictwa koncepcje hello w kolejnych sekcjach hello będzie zrozumieć przykłady hello przydatne.


* Tworzenie i usuwanie udziałów plików Azure
* Tworzenie i usuwanie katalogów
* Wyliczanie plików i katalogów w udziale plików Azure
* Przekazywanie, pobieranie i usuwanie pliku
* Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików platformy Azure
* Utwórz sygnaturę dostępu współdzielonego (SAS klucza) dla pliku, która używa zasad dostępu współdzielonego zdefiniowanych w udziale hello.

> [!Note]  
> Ponieważ magazyn plików Azure mogą uzyskiwać dostęp za pośrednictwem protokołu SMB, jest możliwe toowrite proste aplikacje, które uzyskują dostęp do udziału plików Azure hello przy użyciu hello standard C++ we/wy klasy i funkcje. W tym artykule opisano, jak toowrite aplikacji, które używają hello Azure C++ zestawu SDK usługi Magazyn, który używa hello [interfejsu API REST usługi Magazyn plików Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tooAzure tootalk magazynu plików.

## <a name="create-a-c-application"></a>Tworzenie aplikacji C++
Przykłady hello toobuild, konieczne będzie hello tooinstall 2.4.0 biblioteki klienta magazynu Azure dla języka C++. Należy również utworzono konto magazynu platformy Azure.

tooinstall powitania klienta magazynu Azure 2.4.0 dla języka C++, można użyć jednej z następujących metod hello:

* **Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.
* **System Windows:** w programie Visual Studio, kliknij przycisk **narzędzia &gt; Menedżera pakietów NuGet &gt; Konsola Menedżera pakietów**. Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Konfigurowanie sieci toouse aplikacji usługi Magazyn plików Azure
Dodaj następujące hello wlicza się toohello instrukcje na początku pliku źródłowego C++ hello miejscu toomanipulate usługi Magazyn plików Azure:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Konfigurowanie parametrów połączenia usługi Azure storage
toouse pliku magazynu, musisz mieć konto magazynu Azure tooyour tooconnect. Witaj pierwszym krokiem będzie tooconfigure parametry połączenia, które będą używane konto magazynu tooyour tooconnect. Umożliwia definiowanie statycznego toodo zmiennej który.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Łączenie z kontem magazynu platformy Azure tooan
Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu. tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Tworzenie udziału plików platformy Azure
Wszystkich plików i katalogów w usłudze magazyn plików Azure znajdują się w kontenerze o nazwie **udziału**. Twoje konto magazynu może mieć dowolną liczbę akcji zezwala pojemności Twojego konta. tooobtain dostępu tooa udziału i jego zawartość, należy toouse klienta magazyn plików Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Za pomocą klienta magazyn plików Azure hello można następnie uzyskać udziału tooa odwołania.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

toocreate hello udziału, użyj hello **create_if_not_exists** metody hello **cloud_file_share** obiektu.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

W tym momencie **udostępnianie** posiada udział tooa odwołania o nazwie **Moje udziału próbki**.

## <a name="delete-an-azure-file-share"></a>Usuń udział plików Azure
Usuwanie udziału jest realizowane przez wywołanie hello **delete_if_exists** metody dla obiekt cloud_file_share. Oto przykładowy kod, który robi to.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Tworzenie katalogu
Magazyn można organizować przez umieszczenie plików w podkatalogach zamiast wszystkich z nich w katalogu głównym hello. Magazyn plików Azure umożliwia toocreate dopuszcza wiele katalogów jako Twoje konto zostanie. Poniższy kod Hello utworzy katalog o nazwie **Moje katalog przykładu** w obszarze katalogu głównego hello, a także podkatalogu o nazwie **Moje podkatalogu próbki**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Usuwanie katalogu
Usunięcie katalogu jest prostym zadaniem, chociaż należy zauważyć, że nie można usunąć katalogu, w którym nadal zawiera pliki lub katalogi innych.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Wyliczanie plików i katalogów w udziale plików Azure
Uzyskiwanie listy plików i katalogów w udziale łatwo odbywa się przez wywołanie metody **list_files_and_directories** na **cloud_file_directory** odwołania. bogaty zestaw właściwości i metod zwróconego hello tooaccess **list_file_and_directory_item**, należy wywołać hello **list_file_and_directory_item.as_file** tooget metody **cloud_ plik** obiektu lub hello **list_file_and_directory_item.as_directory** tooget metody **cloud_file_directory** obiektu.

Witaj następującego kodu pokazano, jak tooretrieve i dane wyjściowe hello identyfikatora URI poszczególnych elementów w katalogu głównym hello hello udziału.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Przekazywanie pliku
W bardzo hello najmniej udział plików Azure zawiera katalog główny, w którym mogą znajdować się pliki. W tej sekcji dowiesz się, jak tooupload pliku z magazynu lokalnego na powitania główny katalog udziału.

pierwszym krokiem Hello przekazywania pliku jest tooobtain katalogu toohello odwołania, gdzie powinien znajdować się. W tym celu wywoływania hello **get_root_directory_reference** metody hello udziału obiektu.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Teraz, gdy masz katalog główny odwołania toohello hello udziału, możesz przekazać plik na niego. W tym przykładzie zostanie przesłany z pliku, tekst i ze strumienia.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Pobieranie pliku
pliki toodownload najpierw pobrać odwołanie do pliku, a następnie wywołać hello **download_to_stream** metody tootransfer hello pliku zawartość tooa strumienia obiektu, który można następnie zachować tooa pliku lokalnego. Alternatywnie można użyć hello **download_to_file** metody toodownload hello zawartości pliku lokalnego tooa pliku. Można użyć hello **download_text** metody toodownload hello zawartość pliku jako ciąg tekstowy.

Witaj poniższym przykładzie użyto hello **download_to_stream** i **download_text** toodemonstrate metod pobierania hello pliki, które zostały utworzone w poprzednich sekcjach.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Usuwanie pliku
Inna operacja magazynu plików Azure wspólnej jest usuwanie plików. Witaj następujący kod usuwa plik o nazwie my próbki pliku-3 przechowywane w katalogu głównym hello.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Ustaw hello przydziału (maksymalnego rozmiaru) udziału plików platformy Azure
Można ustawić przydziału hello (lub maksymalny rozmiar) udziału plików w gigabajtach. Można również sprawdzić, jak dużo danych jest obecnie przechowywanych w udziale hello toosee.

Przez ustawienie hello limitu przydziału dla udziału można ograniczyć całkowity rozmiar plików hello przechowywanych w udziale hello hello. Jeśli całkowity rozmiar plików w udziale hello hello przekracza przydział hello ustawiony na powitania udziału, a następnie klienci będą tooincrease hello rozmiaru istniejących plików lub tworzenia nowych plików, chyba że te pliki są puste.

w poniższym przykładzie Hello pokazuje, jak toocheck hello bieżące użycie udziału oraz jak tooset hello przydziału udziału hello.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generowanie sygnatury dostępu współdzielonego dla pliku lub udziału plików
Możesz wygenerować sygnaturę dostępu współdzielonego (SAS) dla udziału plików lub dla pojedynczego pliku. Można również tworzyć zasady dostępu współużytkowanego na dostęp do udostępnionych toomanage udziału plików podpisy. Tworzenie zasad dostępu współdzielonego jest zalecane, ponieważ umożliwia cofnięcie hello SAS, jeśli powinien być zagrożone.

Hello poniższy przykład tworzy zasady dostępu współdzielonego w udziale, a następnie używa, że zasady tooprovide hello ograniczenia na sygnatury dostępu Współdzielonego w pliku w hello udostępniać.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Azure Storage, zapoznaj się z tymi zasobami:

* [Biblioteka klienta usługi Storage dla języka C++](https://github.com/Azure/azure-storage-cpp)
* [Magazynu azure pliku usługi przykłady w języku C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Storage Explorer](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)