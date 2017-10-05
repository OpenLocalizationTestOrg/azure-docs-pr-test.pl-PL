---
title: "Jak używać magazynu obiektów Blob (obiekt magazynu) w języku Ruby | Dokumentacja firmy Microsoft"
description: "Przechowuj dane niestrukturalne w chmurze za pomocą Magazynu obiektów blob Azure."
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
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="be747-103">Jak używać Magazynu obiektów Blob w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="be747-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="be747-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="be747-104">Overview</span></span>
<span data-ttu-id="be747-105">Magazyn obiektów blob Azure jest usługą służącą do przechowywania danych niestrukturalnych w chmurze w postaci obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="be747-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="be747-106">Magazyn obiektów blob umożliwia przechowywanie dowolnego typu danych tekstowych lub binarnych, takich jak dokumenty, pliki multimedialne lub instalatory aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be747-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="be747-107">Magazyn obiektów blob jest również nazywany magazynem obiektów.</span><span class="sxs-lookup"><span data-stu-id="be747-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="be747-108">W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="be747-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="be747-109">Przykłady są napisane przy użyciu interfejsu API Ruby.</span><span class="sxs-lookup"><span data-stu-id="be747-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="be747-110">Omówione scenariusze obejmują **przekazywania, wyświetlanie, pobieranie,** i **usuwanie** obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="be747-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="be747-111">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="be747-111">Create a Ruby application</span></span>
<span data-ttu-id="be747-112">Utwórz aplikację dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="be747-112">Create a Ruby application.</span></span> <span data-ttu-id="be747-113">Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="be747-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="be747-114">Konfigurowanie aplikacji dostęp do magazynu</span><span class="sxs-lookup"><span data-stu-id="be747-114">Configure your application to access Storage</span></span>
<span data-ttu-id="be747-115">Aby korzystać z usługi Azure Storage, konieczne pobranie i użycie dopisków fonetycznych pakiet azure zawiera zestaw wygody bibliotek, które komunikują się z magazynu usługi REST.</span><span class="sxs-lookup"><span data-stu-id="be747-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="be747-116">Umożliwia uzyskanie pakietu RubyGems</span><span class="sxs-lookup"><span data-stu-id="be747-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="be747-117">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="be747-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="be747-118">Wpisz "azure gem instalacji" w oknie wiersza polecenia, aby zainstalować gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="be747-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="be747-119">Importowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="be747-119">Import the package</span></span>
<span data-ttu-id="be747-120">Za pomocą edytora tekstu, Dodaj następujący element do góry pliku dopisków fonetycznych, których zamierzasz używać magazynu:</span><span class="sxs-lookup"><span data-stu-id="be747-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="be747-121">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="be747-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="be747-122">Moduł azure odczyta zmiennych środowiskowych **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** informacji wymagane do łączenia się z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="be747-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="be747-123">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie przed użyciem **Azure::Blob::BlobService** następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="be747-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="be747-124">Aby uzyskać te wartości z klasyczny lub Menedżera zasobów konta magazynu w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="be747-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="be747-125">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="be747-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="be747-126">Przejdź do konta magazynu, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="be747-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="be747-127">W bloku ustawienia po prawej stronie, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="be747-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="be747-128">W bloku klucze dostępu pojawia się zostanie wyświetlony klucz dostępu 1 i klucz dostępu 2.</span><span class="sxs-lookup"><span data-stu-id="be747-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="be747-129">Można użyć jednego z tych.</span><span class="sxs-lookup"><span data-stu-id="be747-129">You can use either of these.</span></span>
5. <span data-ttu-id="be747-130">Kliknij ikonę kopiowania, aby skopiować klucz do Schowka.</span><span class="sxs-lookup"><span data-stu-id="be747-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="be747-131">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="be747-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="be747-132">**Azure::Blob::BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="be747-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="be747-133">Aby utworzyć kontener, użyj **utworzyć\_container()** metody.</span><span class="sxs-lookup"><span data-stu-id="be747-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="be747-134">Poniższy przykład kodu tworzy kontener lub drukuje ten błąd, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="be747-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="be747-135">Jeśli chcesz udostępnić pliki w kontenerze, możesz ustawić uprawnienia do kontenera.</span><span class="sxs-lookup"><span data-stu-id="be747-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="be747-136">Można zmodyfikować <strong>utworzyć\_container()</strong> wywołania do przekazania **: publiczny\_dostępu\_poziom** opcji:</span><span class="sxs-lookup"><span data-stu-id="be747-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="be747-137">Prawidłowymi wartościami dla **: publiczny\_dostępu\_poziom** są opcji:</span><span class="sxs-lookup"><span data-stu-id="be747-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="be747-138">**Obiekt blob:** Określa publiczny dostęp do odczytu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="be747-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="be747-139">Mogą być odczytywane dane obiektów blob w tym kontenerze za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera.</span><span class="sxs-lookup"><span data-stu-id="be747-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="be747-140">Klienci nie można wyliczyć obiektów blob w kontenerze, za pomocą żądania od użytkowników anonimowych.</span><span class="sxs-lookup"><span data-stu-id="be747-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="be747-141">**kontener:** określa pełnej publiczny dostęp do odczytu obiektów blob i kontenera danych.</span><span class="sxs-lookup"><span data-stu-id="be747-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="be747-142">Klientów można wyliczyć obiektów blob w kontenerze, za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="be747-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="be747-143">Alternatywnie można zmodyfikować poziomu dostępu publicznego kontenera za pomocą **ustawić\_kontenera\_acl()** metodę, aby określić poziom dostępu publicznego.</span><span class="sxs-lookup"><span data-stu-id="be747-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="be747-144">Poniższy przykład kodu zmienia poziom dostępu publicznego do **kontenera**:</span><span class="sxs-lookup"><span data-stu-id="be747-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="be747-145">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="be747-145">Upload a blob into a container</span></span>
<span data-ttu-id="be747-146">Aby przekazać zawartości do obiektu blob, użyj **utworzyć\_bloku\_blob()** metodę w celu utworzenia obiektu blob, użyj pliku lub ciągu jako zawartość obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="be747-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="be747-147">Poniższy kod powoduje przekazanie pliku **test.png** jako nowy obiekt blob o nazwie "— obiekt blob obrazu" w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="be747-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="be747-148">Wyświetlanie listy obiektów blob w kontenerze</span><span class="sxs-lookup"><span data-stu-id="be747-148">List the blobs in a container</span></span>
<span data-ttu-id="be747-149">Aby wyświetlić listę kontenery, użyj **list_containers()** metody.</span><span class="sxs-lookup"><span data-stu-id="be747-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="be747-150">Aby wyświetlić listę obiektów blob w kontenerze, należy użyć **listy\_blobs()** metody.</span><span class="sxs-lookup"><span data-stu-id="be747-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="be747-151">Generuje to adresy URL wszystkich obiektów blob w kontenerach dla konta.</span><span class="sxs-lookup"><span data-stu-id="be747-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="be747-152">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="be747-152">Download blobs</span></span>
<span data-ttu-id="be747-153">Aby pobrać obiekty BLOB, użyj **uzyskać\_blob()** metody, aby pobrać zawartość.</span><span class="sxs-lookup"><span data-stu-id="be747-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="be747-154">Poniższy przykład kodu pokazuje, za pomocą **uzyskać\_blob()** do pobrania zawartości "obiekt blob obrazu" i zapisz je w pliku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="be747-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="be747-155">Usuwanie obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="be747-155">Delete a Blob</span></span>
<span data-ttu-id="be747-156">Na koniec, aby usunąć obiekt blob, użyj **usunąć\_blob()** metody.</span><span class="sxs-lookup"><span data-stu-id="be747-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="be747-157">Poniższy przykład kodu pokazuje, jak można usunąć obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="be747-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="be747-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be747-158">Next steps</span></span>
<span data-ttu-id="be747-159">Aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu, skorzystaj z poniższych linków:</span><span class="sxs-lookup"><span data-stu-id="be747-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="be747-160">Blog zespołu odpowiedzialnego za usługę Azure Storage</span><span class="sxs-lookup"><span data-stu-id="be747-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="be747-161">[Zestaw Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="be747-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="be747-162">Transfer danych za pomocą narzędzia wiersza polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="be747-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

