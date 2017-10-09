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
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="32458-103">Jak toouse magazynu obiektów Blob w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="32458-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="32458-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="32458-104">Overview</span></span>
<span data-ttu-id="32458-105">Magazyn obiektów Blob Azure to usługa, która przechowywania danych niestrukturalnych w chmurze hello w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="32458-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="32458-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32458-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="32458-107">Magazyn obiektów blob jest również tooas określonego obiektu magazynu.</span><span class="sxs-lookup"><span data-stu-id="32458-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="32458-108">W tym przewodniku opisano, jak tooperform typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="32458-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="32458-109">Hello przykłady są napisane przy użyciu hello Ruby interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="32458-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="32458-110">Witaj omówione scenariusze obejmują **przekazywania, wyświetlanie, pobieranie,** i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="32458-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="32458-111">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="32458-111">Create a Ruby application</span></span>
<span data-ttu-id="32458-112">Utwórz aplikację dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="32458-112">Create a Ruby application.</span></span> <span data-ttu-id="32458-113">Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="32458-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="32458-114">Konfigurowanie sieci tooaccess aplikacji magazynu</span><span class="sxs-lookup"><span data-stu-id="32458-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="32458-115">toouse usługi Azure Storage, należy toodownload i użyj hello dopisków fonetycznych azure pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="32458-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="32458-116">Użyj RubyGems tooobtain hello pakietu</span><span class="sxs-lookup"><span data-stu-id="32458-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="32458-117">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="32458-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="32458-118">Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="32458-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="32458-119">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="32458-119">Import hello package</span></span>
<span data-ttu-id="32458-120">Za pomocą edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="32458-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="32458-121">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="32458-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="32458-122">Moduł Hello azure odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** dla Konto magazynu Azure tooyour tooconnect wymaganych informacji.</span><span class="sxs-lookup"><span data-stu-id="32458-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="32458-123">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::Blob::BlobService** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="32458-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="32458-124">tooobtain te wartości z klasyczny lub Menedżera zasobów magazynu konta w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="32458-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="32458-125">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32458-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="32458-126">Przejdź toohello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="32458-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="32458-127">W bloku ustawienia hello na powitania prawo, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="32458-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="32458-128">W bloku klucze dostępu hello, który pojawia się zostanie wyświetlony klucz dostępu hello 1 i klucz dostępu 2.</span><span class="sxs-lookup"><span data-stu-id="32458-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="32458-129">Można użyć jednego z tych.</span><span class="sxs-lookup"><span data-stu-id="32458-129">You can use either of these.</span></span>
5. <span data-ttu-id="32458-130">Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="32458-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="32458-131">tooobtain te wartości z klasycznym magazynu konta w klasycznym portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="32458-131">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="32458-132">Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="32458-132">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="32458-133">Przejdź toohello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="32458-133">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="32458-134">Kliknij przycisk **ZARZĄDZAJ KLUCZAMI dostępu** u dołu okienka nawigacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="32458-134">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="32458-135">W wyskakującym oknie dialogowym hello zostanie wyświetlona nazwa konta magazynu hello, podstawowy klucz dostępu i pomocniczy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="32458-135">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="32458-136">Klucz dostępu można użyć hello główną lub hello jednej dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="32458-136">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="32458-137">Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="32458-137">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="32458-138">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="32458-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="32458-139">Witaj **Azure::Blob::BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="32458-139">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="32458-140">toocreate kontener, użyj hello **utworzyć\_container()** metody.</span><span class="sxs-lookup"><span data-stu-id="32458-140">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="32458-141">Witaj poniższy przykład kodu tworzy kontener lub drukuje hello błąd, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="32458-141">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="32458-142">Jeśli chcesz toomake hello pliki w kontenerze hello publiczne, możesz ustawić uprawnienia hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="32458-142">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="32458-143">Można modyfikować tylko hello <strong>utworzyć\_container()</strong> hello toopass wywołania **: publiczny\_dostępu\_poziom** opcji:</span><span class="sxs-lookup"><span data-stu-id="32458-143">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="32458-144">Prawidłowe wartości hello **: publiczny\_dostępu\_poziom** są opcji:</span><span class="sxs-lookup"><span data-stu-id="32458-144">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="32458-145">**Obiekt blob:** Określa publiczny dostęp do odczytu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="32458-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="32458-146">Mogą być odczytywane dane obiektów blob w tym kontenerze za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="32458-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="32458-147">Klienci nie można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="32458-147">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="32458-148">**kontener:** określa pełnej publiczny dostęp do odczytu obiektów blob i kontenera danych.</span><span class="sxs-lookup"><span data-stu-id="32458-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="32458-149">Klientów można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="32458-149">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="32458-150">Alternatywnie można zmodyfikować poziomu dostępu publicznego hello kontenera za pomocą **ustawić\_kontenera\_acl()** poziom dostępu publicznego hello toospecify metody.</span><span class="sxs-lookup"><span data-stu-id="32458-150">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="32458-151">Witaj, poniższy przykład kodu zmiany hello zbyt poziomie dostępu publicznego**kontenera**:</span><span class="sxs-lookup"><span data-stu-id="32458-151">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="32458-152">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="32458-152">Upload a blob into a container</span></span>
<span data-ttu-id="32458-153">tooupload zawartości tooa blob, użyj hello **utworzyć\_bloku\_blob()** obiektu blob hello toocreate metody, przy użyciu pliku lub string jako zawartość hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="32458-153">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="32458-154">Witaj następujący kod plik zostanie przesłany hello **test.png** jako nowy obiekt blob o nazwie "— obiekt blob obrazu" w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="32458-154">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="32458-155">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="32458-155">List hello blobs in a container</span></span>
<span data-ttu-id="32458-156">toolist hello kontenery, użyj **list_containers()** metody.</span><span class="sxs-lookup"><span data-stu-id="32458-156">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="32458-157">Użyj toolist hello BLOB w kontenerze, **listy\_blobs()** metody.</span><span class="sxs-lookup"><span data-stu-id="32458-157">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="32458-158">To generuje hello adresy URL wszystkich hello obiektów blob w wszystkich kontenerów hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="32458-158">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="32458-159">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="32458-159">Download blobs</span></span>
<span data-ttu-id="32458-160">toodownload obiektów blob, użyj hello **uzyskać\_blob()** metody tooretrieve hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="32458-160">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="32458-161">Witaj poniższy przykład kodu pokazuje przy użyciu **uzyskać\_blob()** toodownload hello zawartość "obiekt blob obrazu" i Zapisz plik lokalny tooa.</span><span class="sxs-lookup"><span data-stu-id="32458-161">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="32458-162">Usuwanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="32458-162">Delete a Blob</span></span>
<span data-ttu-id="32458-163">Na koniec toodelete obiektu blob, użyj hello **usunąć\_blob()** metody.</span><span class="sxs-lookup"><span data-stu-id="32458-163">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="32458-164">Witaj poniższy przykład kodu pokazuje sposób toodelete obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="32458-164">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="32458-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32458-165">Next steps</span></span>
<span data-ttu-id="32458-166">toolearn o bardziej skomplikowanych zadaniach magazynu, skorzystaj z poniższych linków:</span><span class="sxs-lookup"><span data-stu-id="32458-166">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="32458-167">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="32458-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="32458-168">[Zestaw Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="32458-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="32458-169">Transfer danych za pomocą wiersza polecenia Azcopy hello</span><span class="sxs-lookup"><span data-stu-id="32458-169">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

