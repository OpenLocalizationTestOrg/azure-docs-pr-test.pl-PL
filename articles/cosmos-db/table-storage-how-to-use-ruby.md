---
title: "toouse aaaHow Azure Table Storage w języku Ruby | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="30cb3-103">Jak toouse Azure Table Storage w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="30cb3-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="30cb3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="30cb3-104">Overview</span></span>
<span data-ttu-id="30cb3-105">Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="30cb3-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="30cb3-106">Hello przykłady są napisane przy użyciu hello Ruby interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="30cb3-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="30cb3-107">Witaj omówione scenariusze obejmują **tworzenie i usuwanie tabeli, wstawianie i badania jednostek w tabeli**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="30cb3-108">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="30cb3-108">Create a Ruby application</span></span>
<span data-ttu-id="30cb3-109">Aby uzyskać instrukcje jak toocreate dopisków fonetycznych aplikacji, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="30cb3-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="30cb3-110">Konfigurowanie sieci tooaccess aplikacji magazynu</span><span class="sxs-lookup"><span data-stu-id="30cb3-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="30cb3-111">toouse usługi Azure Storage, należy toodownload i użyj hello dopisków fonetycznych pakiet azure, która zawiera zestaw wygody bibliotek, które komunikują się z usługami REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="30cb3-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="30cb3-112">Użyj RubyGems tooobtain hello pakietu</span><span class="sxs-lookup"><span data-stu-id="30cb3-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="30cb3-113">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="30cb3-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="30cb3-114">Typ **azure instalacji gem** hello polecenia okna tooinstall hello gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="30cb3-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="30cb3-115">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="30cb3-115">Import hello package</span></span>
<span data-ttu-id="30cb3-116">Użyj edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="30cb3-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="30cb3-117">Konfigurowanie połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="30cb3-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="30cb3-118">Hello azure modułu odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza**informacje wymagane konto usługi Azure Storage tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="30cb3-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="30cb3-119">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::TableService** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="30cb3-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="30cb3-120">tooobtain te wartości z klasyczny lub Menedżera zasobów magazynu konta w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="30cb3-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="30cb3-121">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30cb3-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="30cb3-122">Przejdź toohello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="30cb3-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="30cb3-123">W bloku ustawienia hello na powitania prawo, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="30cb3-124">W bloku klucze dostępu hello, który pojawia się zostanie wyświetlony klucz dostępu hello 1 i klucz dostępu 2.</span><span class="sxs-lookup"><span data-stu-id="30cb3-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="30cb3-125">Można użyć jednego z tych.</span><span class="sxs-lookup"><span data-stu-id="30cb3-125">You can use either of these.</span></span>
5. <span data-ttu-id="30cb3-126">Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="30cb3-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="30cb3-127">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="30cb3-127">Create a table</span></span>
<span data-ttu-id="30cb3-128">Witaj **Azure::TableService** obiektu umożliwia pracę z tabel i jednostek.</span><span class="sxs-lookup"><span data-stu-id="30cb3-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="30cb3-129">toocreate tabelę, użyj hello **utworzyć\_table()** metody.</span><span class="sxs-lookup"><span data-stu-id="30cb3-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="30cb3-130">Witaj poniższy przykład tworzy tabelę lub odbitek hello błąd, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="30cb3-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="30cb3-131">Dodaj tabelę tooa jednostki</span><span class="sxs-lookup"><span data-stu-id="30cb3-131">Add an entity tooa table</span></span>
<span data-ttu-id="30cb3-132">tooadd jednostki, najpierw utworzyć obiektu skrótu, który definiuje właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="30cb3-133">Należy zauważyć, że dla każdej jednostki można określić **PartitionKey** i **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="30cb3-134">Są to hello unikatowych identyfikatorów jednostki które są wartości, które można wykonać zapytania znacznie szybciej niż inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="30cb3-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="30cb3-135">Usługa Azure Storage korzysta **PartitionKey** tooautomatically rozpowszechniać jednostek tabeli hello przez wiele węzłów magazynu.</span><span class="sxs-lookup"><span data-stu-id="30cb3-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="30cb3-136">Jednostki z hello sam **PartitionKey** są przechowywane na powitania tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="30cb3-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="30cb3-137">Witaj **RowKey** jest unikatowy identyfikator hello hello jednostek w partycji hello należy.</span><span class="sxs-lookup"><span data-stu-id="30cb3-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="30cb3-138">Aktualizuj jednostkę</span><span class="sxs-lookup"><span data-stu-id="30cb3-138">Update an entity</span></span>
<span data-ttu-id="30cb3-139">Istnieje wiele metod tooupdate dostępne istniejącego obiektu:</span><span class="sxs-lookup"><span data-stu-id="30cb3-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="30cb3-140">**Zaktualizuj\_entity():** zaktualizowania istniejącej jednostki poprzez zastąpienie jej.</span><span class="sxs-lookup"><span data-stu-id="30cb3-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="30cb3-141">**Scalanie\_entity():** aktualizacji przez scalenie nowej wartości właściwości istniejącej jednostki hello istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="30cb3-142">**Wstaw\_lub\_scalania\_entity():** aktualizacji przez zastąpienie istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="30cb3-143">Jeśli jednostka nie istnieje, zostanie wstawiony nowy:</span><span class="sxs-lookup"><span data-stu-id="30cb3-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="30cb3-144">**Wstaw\_lub\_Zastąp\_entity():** aktualizacji przez scalenie nowej wartości właściwości istniejącej jednostki hello istniejącej jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="30cb3-145">Jeśli jednostka nie istnieje, zostanie wstawiony nowy.</span><span class="sxs-lookup"><span data-stu-id="30cb3-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="30cb3-146">Witaj poniższym przykładzie pokazano aktualizowanie jednostki przy użyciu **aktualizacji\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="30cb3-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="30cb3-147">Z **aktualizacji\_entity()** i **scalania\_entity()**, jeśli jednostka hello, aktualizowanego nie istnieje hello operacji aktualizacji zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="30cb3-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="30cb3-148">W związku z tym jeśli toostore jednostki niezależnie od tego, czy już istnieje, należy zamiast tego używać **Wstaw\_lub\_Zastąp\_entity()** lub **Wstaw\_lub \_scalania\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="30cb3-149">Praca z grupami jednostek</span><span class="sxs-lookup"><span data-stu-id="30cb3-149">Work with groups of entities</span></span>
<span data-ttu-id="30cb3-150">Czasami powoduje toosubmit znaczeniu wiele operacji razem w tooensure partii przetwarzania przez serwer hello atomic.</span><span class="sxs-lookup"><span data-stu-id="30cb3-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="30cb3-151">tooaccomplish, aby najpierw utworzyć **partii** obiekt, a następnie użyj hello **wykonania\_batch()** metoda **TableService**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="30cb3-152">Witaj poniższym przykładzie pokazano przesyłanie dwie jednostki z RowKey 2 i 3 w partii.</span><span class="sxs-lookup"><span data-stu-id="30cb3-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="30cb3-153">Zwróć uwagę że tylko działania dla jednostek o hello PartitionKey tego samego.</span><span class="sxs-lookup"><span data-stu-id="30cb3-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="30cb3-154">Zapytanie dla jednostki</span><span class="sxs-lookup"><span data-stu-id="30cb3-154">Query for an entity</span></span>
<span data-ttu-id="30cb3-155">tooquery jednostkę w tabeli, użyj hello **uzyskać\_entity()** metody, przekazując nazwy tabeli hello, **PartitionKey** i **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="30cb3-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="30cb3-156">Zapytanie zestawu jednostek</span><span class="sxs-lookup"><span data-stu-id="30cb3-156">Query a set of entities</span></span>
<span data-ttu-id="30cb3-157">tooquery zestawu jednostek w tabeli, utworzyć obiektu skrótu zapytania i użyj hello **zapytania\_entities()** metody.</span><span class="sxs-lookup"><span data-stu-id="30cb3-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="30cb3-158">Witaj poniższym przykładzie pokazano pobieranie wszystkich jednostek hello z hello tego samego **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="30cb3-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="30cb3-159">Zestaw wyników hello jest zbyt duży dla tooreturn jednego zapytania, token kontynuacji zostaną zwrócone którego można użyć tooretrieve kolejnych stronach.</span><span class="sxs-lookup"><span data-stu-id="30cb3-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="30cb3-160">Tworzenie zapytania do podzbioru właściwości jednostki</span><span class="sxs-lookup"><span data-stu-id="30cb3-160">Query a subset of entity properties</span></span>
<span data-ttu-id="30cb3-161">Tabela tooa kwerend może pobrać kilka właściwości jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="30cb3-162">Ta technika, zwana "projekcji", redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek.</span><span class="sxs-lookup"><span data-stu-id="30cb3-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="30cb3-163">Klauzula select hello użycia i nazwy hello przebiegu hello właściwości chcesz toobring toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="30cb3-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="30cb3-164">Usuwanie jednostki</span><span class="sxs-lookup"><span data-stu-id="30cb3-164">Delete an entity</span></span>
<span data-ttu-id="30cb3-165">toodelete jednostkę, użyj hello **usunąć\_entity()** metody.</span><span class="sxs-lookup"><span data-stu-id="30cb3-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="30cb3-166">Należy toopass w hello nazwy tabeli hello, która zawiera jednostki hello, hello PartitionKey i RowKey hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="30cb3-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="30cb3-167">Usuwanie tabeli</span><span class="sxs-lookup"><span data-stu-id="30cb3-167">Delete a table</span></span>
<span data-ttu-id="30cb3-168">toodelete tabelę, użyj hello **usunąć\_table()** — metoda i przekaż nazwę hello hello tabelę, która ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="30cb3-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="30cb3-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30cb3-169">Next steps</span></span>

* <span data-ttu-id="30cb3-170">[Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="30cb3-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="30cb3-171">[Zestaw Azure SDK dla środowiska Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="30cb3-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

