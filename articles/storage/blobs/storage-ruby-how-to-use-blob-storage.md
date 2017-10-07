---
title: "toouse aaaHow obiektu Blob magazynu (obiekt) w języku Ruby | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze hello z magazynu obiektów Blob platformy Azure (obiekt magazynu)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Jak toouse magazynu obiektów Blob w języku Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob. Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.

W tym przewodniku opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob. Hello przykłady są napisane przy użyciu hello Ruby interfejsu API. Witaj omówione scenariusze obejmują **przekazywania, wyświetlanie, pobieranie,** i **usuwanie** obiektów blob.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Tworzenie aplikacji Ruby
Utwórz aplikację dopisków fonetycznych. Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu
toouse usługi Azure Storage, należy toodownload i użyj hello dopisków fonetycznych azure pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Użyj RubyGems tooobtain hello pakietu
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).
2. Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Za pomocą edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
Moduł Hello azure odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** dla Konto magazynu Azure tooyour tooconnect wymaganych informacji. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::Blob::BlobService** z hello następującego kodu:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain te wartości z klasyczny lub Menedżera zasobów magazynu konta w portalu Azure hello:

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).
2. Przejdź toohello konta magazynu, które chcesz toouse.
3. W bloku ustawienia hello na powitania prawo, kliknij przycisk **klucze dostępu**.
4. W bloku klucze dostępu hello, który pojawia się zostanie wyświetlony klucz dostępu hello 1 i klucz dostępu 2. Można użyć jednego z tych.
5. Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.

## <a name="create-a-container"></a>Tworzenie kontenera
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Witaj **Azure::Blob::BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob. toocreate kontener, użyj hello **utworzyć\_container()** metody.

Witaj poniższy przykład kodu tworzy kontener lub drukuje hello błąd, jeśli istnieje.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Jeśli chcesz toomake hello pliki w kontenerze hello publiczne, możesz ustawić uprawnienia hello kontenera.

Można modyfikować tylko hello <strong>utworzyć\_container()</strong> hello toopass wywołania **: publiczny\_dostępu\_poziom** opcji:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Prawidłowe wartości hello **: publiczny\_dostępu\_poziom** są opcji:

* **Obiekt blob:** Określa publiczny dostęp do odczytu obiektów blob. Mogą być odczytywane dane obiektów blob w tym kontenerze za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera. Klienci nie można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych.
* **kontener:** określa pełnej publiczny dostęp do odczytu obiektów blob i kontenera danych. Klientów można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.

Alternatywnie można zmodyfikować poziomu dostępu publicznego hello kontenera za pomocą **ustawić\_kontenera\_acl()** poziom dostępu publicznego hello toospecify metody.

Witaj, poniższy przykład kodu zmiany hello zbyt poziomie dostępu publicznego**kontenera**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Przekazywanie obiektu blob do kontenera
tooupload zawartości tooa blob, użyj hello **utworzyć\_bloku\_blob()** obiektu blob hello toocreate metody, przy użyciu pliku lub string jako zawartość hello hello obiektu blob.

Witaj następujący kod plik zostanie przesłany hello **test.png** jako nowy obiekt blob o nazwie "— obiekt blob obrazu" w kontenerze hello.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Lista hello BLOB w kontenerze
toolist hello kontenery, użyj **list_containers()** metody.
Użyj toolist hello BLOB w kontenerze, **listy\_blobs()** metody.

To generuje hello adresy URL wszystkich hello obiektów blob w wszystkich kontenerów hello hello konta.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Pobieranie obiektów blob
toodownload obiektów blob, użyj hello **uzyskać\_blob()** metody tooretrieve hello zawartość.

Witaj poniższy przykład kodu pokazuje przy użyciu **uzyskać\_blob()** toodownload hello zawartość "obiekt blob obrazu" i Zapisz plik lokalny tooa.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Usuwanie obiektu Blob
Na koniec toodelete obiektu blob, użyj hello **usunąć\_blob()** metody. Witaj poniższy przykład kodu pokazuje sposób toodelete obiektu blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Następne kroki
toolearn o bardziej skomplikowanych zadaniach magazynu, skorzystaj z poniższych linków:

* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Zestaw Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

