---
title: "toouse aaaHow Azure Table Storage w języku Ruby | Dokumentacja firmy Microsoft"
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Jak toouse Azure Table Storage w języku Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi tabel Azure. Hello przykłady są napisane przy użyciu hello Ruby interfejsu API. Witaj omówione scenariusze obejmują **tworzenie i usuwanie tabeli, wstawianie i badania jednostek w tabeli**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Tworzenie aplikacji Ruby
Aby uzyskać instrukcje jak toocreate dopisków fonetycznych aplikacji, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu
toouse usługi Azure Storage, należy toodownload i użyj hello dopisków fonetycznych pakiet azure, która zawiera zestaw wygody bibliotek, które komunikują się z usługami REST magazynu hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Użyj RubyGems tooobtain hello pakietu
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).
2. Typ **azure instalacji gem** hello polecenia okna tooinstall hello gem i zależności.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Użyj edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Konfigurowanie połączenia z magazynem Azure
Hello azure modułu odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_dostępu\_klucza**informacje wymagane konto usługi Azure Storage tooyour tooconnect. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::TableService** z hello następującego kodu:

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

tooobtain te wartości z klasycznym magazynu konta w klasycznym portalu Azure hello:

1. Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź toohello konta magazynu, które chcesz toouse.
3. Kliknij przycisk **ZARZĄDZAJ KLUCZAMI dostępu** u dołu okienka nawigacji hello hello.
4. W wyskakującym oknie dialogowym hello zostanie wyświetlona nazwa konta magazynu hello, podstawowy klucz dostępu i pomocniczy klucz dostępu. Klucz dostępu można użyć hello główną lub hello jednej dodatkowej.
5. Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.

## <a name="create-a-table"></a>Tworzenie tabeli
Witaj **Azure::TableService** obiektu umożliwia pracę z tabel i jednostek. toocreate tabelę, użyj hello **utworzyć\_table()** metody. Witaj poniższy przykład tworzy tabelę lub odbitek hello błąd, jeśli istnieje.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
tooadd jednostki, najpierw utworzyć obiektu skrótu, który definiuje właściwości jednostki. Należy zauważyć, że dla każdej jednostki można określić **PartitionKey** i **RowKey**. Są to hello unikatowych identyfikatorów jednostki które są wartości, które można wykonać zapytania znacznie szybciej niż inne właściwości. Usługa Azure Storage korzysta **PartitionKey** tooautomatically rozpowszechniać jednostek tabeli hello przez wiele węzłów magazynu. Jednostki z hello sam **PartitionKey** są przechowywane na powitania tym samym węźle. Witaj **RowKey** jest unikatowy identyfikator hello hello jednostek w partycji hello należy.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Aktualizuj jednostkę
Istnieje wiele metod tooupdate dostępne istniejącego obiektu:

* **Zaktualizuj\_entity():** zaktualizowania istniejącej jednostki poprzez zastąpienie jej.
* **Scalanie\_entity():** aktualizacji przez scalenie nowej wartości właściwości istniejącej jednostki hello istniejącej jednostki.
* **Wstaw\_lub\_scalania\_entity():** aktualizacji przez zastąpienie istniejącej jednostki. Jeśli jednostka nie istnieje, zostanie wstawiony nowy:
* **Wstaw\_lub\_Zastąp\_entity():** aktualizacji przez scalenie nowej wartości właściwości istniejącej jednostki hello istniejącej jednostki. Jeśli jednostka nie istnieje, zostanie wstawiony nowy.

Witaj poniższym przykładzie pokazano aktualizowanie jednostki przy użyciu **aktualizacji\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Z **aktualizacji\_entity()** i **scalania\_entity()**, jeśli jednostka hello, aktualizowanego nie istnieje hello operacji aktualizacji zakończy się niepowodzeniem. W związku z tym jeśli toostore jednostki niezależnie od tego, czy już istnieje, należy zamiast tego używać **Wstaw\_lub\_Zastąp\_entity()** lub **Wstaw\_lub \_scalania\_entity()**.

## <a name="work-with-groups-of-entities"></a>Praca z grupami jednostek
Czasami powoduje toosubmit znaczeniu wiele operacji razem w tooensure partii przetwarzania przez serwer hello atomic. tooaccomplish, aby najpierw utworzyć **partii** obiekt, a następnie użyj hello **wykonania\_batch()** metoda **TableService**. Witaj poniższym przykładzie pokazano przesyłanie dwie jednostki z RowKey 2 i 3 w partii. Zwróć uwagę że tylko działania dla jednostek o hello PartitionKey tego samego.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Zapytanie dla jednostki
tooquery jednostkę w tabeli, użyj hello **uzyskać\_entity()** metody, przekazując nazwy tabeli hello, **PartitionKey** i **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Zapytanie zestawu jednostek
tooquery zestawu jednostek w tabeli, utworzyć obiektu skrótu zapytania i użyj hello **zapytania\_entities()** metody. Witaj poniższym przykładzie pokazano pobieranie wszystkich jednostek hello z hello tego samego **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Zestaw wyników hello jest zbyt duży dla tooreturn jednego zapytania, token kontynuacji zostaną zwrócone którego można użyć tooretrieve kolejnych stronach.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Tworzenie zapytania do podzbioru właściwości jednostki
Tabela tooa kwerend może pobrać kilka właściwości jednostki. Ta technika, zwana "projekcji", redukuje przepustowość i może poprawiać wydajność zapytań, zwłaszcza w przypadku dużych jednostek. Klauzula select hello użycia i nazwy hello przebiegu hello właściwości chcesz toobring toohello klienta.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Usuwanie jednostki
toodelete jednostkę, użyj hello **usunąć\_entity()** metody. Należy toopass w hello nazwy tabeli hello, która zawiera jednostki hello, hello PartitionKey i RowKey hello jednostki.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Usuwanie tabeli
toodelete tabelę, użyj hello **usunąć\_table()** — metoda i przekaż nazwę hello hello tabelę, która ma toodelete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Następne kroki

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Zestaw Azure SDK dla środowiska Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub

