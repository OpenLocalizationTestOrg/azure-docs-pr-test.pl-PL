---
title: toouse aaaHow Table storage (C++) | Dokumentacja firmy Microsoft
description: "Przechowywanie danych strukturalnych w chmurze hello przy użyciu magazynu tabel Azure, Magazyn danych NoSQL."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Jak toouse magazynu tabel w języku C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi Magazyn tabel Azure. Hello przykłady są napisane w języku C++ i używają hello [biblioteki klienta usługi Azure Storage dla języka C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Witaj omówione scenariusze obejmują **tworzenia i usuwania tabeli** i **Praca z jednostek tabeli**.

> [!NOTE]
> Cele tego przewodnika hello biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej. Hello zalecana jest wersja biblioteki klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Tworzenie aplikacji C++
W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++. toodo tak, konieczne będzie tooinstall hello biblioteki klienta magazynu Azure dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.  

Witaj tooinstall biblioteki klienta magazynu Azure dla języka C++, można użyć hello następujące metody:

* **Linux:** postępuj zgodnie z instrukcjami hello hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.  
* **System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**. Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz Enter.  
  
     Pakiet instalacyjny wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu tabel
Dodaj następujące hello wlicza się instrukcje toohello górnej części pliku C++ hello miejscu toouse hello magazynu Azure API tooaccess tabel:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Konfigurowanie parametrów połączenia usługi Azure storage
Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania aplikacji klienckiej, musisz podać parametry połączenia magazynu hello w hello zgodny z formatem. Użyj hello nazwę konta i hello magazynu klucz dostępu do magazynu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com) dla hello *AccountName* i *AccountKey* wartości. Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [kont magazynu Azure o](storage-create-storage-account.md). Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest aplikacji w lokalnym komputerze z systemem Windows można użyć hello Azure [emulatora magazynu](storage-use-emulator.md) zainstalowane z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/). emulator magazynu Hello jest narzędziem, która symuluje hello dostępne na komputerze deweloperskim lokalnej usługi obiektów Blob platformy Azure, kolejki i tabeli. Witaj poniższym przykładzie pokazano, jak można zadeklarować pola statycznego toohold hello połączenia ciąg tooyour lokalnym emulatorze magazynu:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello emulatora magazynu Azure, kliknij przycisk hello **Start** przycisk lub naciśnij klawisz systemu Windows hello. Rozpocznij wpisywanie **emulatora magazynu Azure**, a następnie wybierz **emulatora magazynu Azure Microsoft** z listy aplikacji hello.  

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.  

## <a name="retrieve-your-connection-string"></a>Pobranie parametrów połączenia
Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu. tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello metody parse.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Następnie Pobierz tooa odwołanie **cloud_table_client** klasy, ponieważ pozwala uzyskać obiekty odwołania do tabel i jednostek przechowywanych w hello usługi Magazyn tabel. Witaj poniższy kod tworzy **cloud_table_client** obiektu za pomocą obiektu konta magazynu hello możemy pobrać powyżej:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Tworzenie tabeli
A **cloud_table_client** obiektu pozwala pobierać obiekty odwołania do tabel i jednostek. Witaj poniższy kod tworzy **cloud_table_client** obiektu i używa go toocreate nową tabelę.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Dodaj tabelę tooa jednostki
tooadd tabeli tooa jednostki, Utwórz nową **table_entity** obiektu i przekaż go za**table_operation::insert_entity**. Witaj poniższy kod używa imienia klienta hello jako hello klucz wiersza i nazwiska jako klucza partycji hello. Razem klucz partycji i klucz wiersza jednoznacznie zidentyfikować hello jednostki w tabeli hello. Klucze partycji jednostki z tym samym kluczem partycji mogą być przeszukiwane szybciej niż jednostki o różnych powitalne, ale przy użyciu różnych kluczy partycji umożliwia zwiększenie skalowalności operacji równoległych. Aby uzyskać więcej informacji, zobacz [kontrolną wydajności i skalowalności magazynu Microsoft Azure](storage-performance-checklist.md).

Witaj poniższy kod tworzy nowe wystąpienie klasy **table_entity** z niektórych toobe dane klienta przechowywane. Witaj kod wywołuje dalej **table_operation::insert_entity** toocreate **table_operation** obiekt tooinsert jednostki do tabeli, a skojarzone hello nową jednostkę tabeli z nim. Na koniec kod hello wywołuje hello wykonać metody na powitania **cloud_table** obiektu. I hello nowe **table_operation** wysyła żądanie toohello usługi tooinsert hello nowego klienta jednostkę tabeli do tabeli "osoby" hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Zbiorcze wstawianie jednostek
Możesz wstawić partię jednostek toohello usługi tabel w jednej operacji zapisu. Witaj poniższy kod tworzy **table_batch_operation** obiekt, a następnie dodanie trzy Wstaw tooit operacji. Każda operacja insert jest dodawany przez utworzenie nowego obiektu jednostki, jego wartości ustawienia i wywołując hello wstawiania metody na powitania **table_batch_operation** obiektu tooassociate hello jednostki o nowej operacji wstawiania. Następnie **cloud_table.execute** jest nazywany tooexecute hello operacji.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Niektóre elementy toonote dotyczące operacji zbiorczych:  

* Można wykonać wstawiania too100, Usuń, scalania, Zamień, operacje wstawiania lub scalania i wstawianie lub zastępowanie w dowolnej kombinacji w pojedynczej partii.  
* Operacji zbiorczej może mieć operacji pobierania, jeśli jest jedyną operacją hello w partii hello.  
* Wszystkie jednostki w jednej operacji zbiorczej muszą mieć hello tego samego klucza partycji.  
* Operacji zbiorczej jest ograniczona tooa 4 MB danych ładunku.  

## <a name="retrieve-all-entities-in-a-partition"></a>Pobieranie wszystkich jednostek w partycji
tooquery tabeli dla wszystkich jednostek w partycji, użyj **table_query** obiektu. Witaj poniższy przykład kodu Określa filtr jednostek, gdzie "Smith" jest hello klucza partycji. W tym przykładzie drukowane hello pola każdej jednostki w konsoli toohello wyników zapytania hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

Witaj zapytania w tym przykładzie powoduje przeniesienie wszystkich jednostek hello spełniające kryteria filtrowania hello. Jeśli korzystasz z dużych tabel i często muszą jednostek tabeli hello toodownload, zaleca się przechowywać dane w obiektach blob magazynu Azure zamiast tego.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Pobieranie zakresu jednostek w partycji
Jeśli nie chcesz tooquery wszystkie hello jednostek w partycji, możesz określić zakres, łącząc filtr klucza partycji hello z filtrem klucza wiersza. Witaj poniższy przykład kodu wykorzystuje dwa filtry tooget wszystkich jednostek w partycji "Smith", gdzie hello klucz wiersza (imię) wcześniejszej niż "E" w alfabecie hello zaczynał się literą, a następnie drukuje wyniki zapytania hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Pobieranie pojedynczej jednostki
Tooretrieve kwerendy można pisać w jednej, określonej jednostki. Witaj poniższy kod używa **table_operation::retrieve_entity** toospecify powitania klienta "Jan Kowalski". Ta metoda zwraca tylko jedną jednostkę zamiast kolekcji i hello zwrócona wartość jest **table_result**. Określenie kluczy partycji i wiersza w zapytaniu jest hello najszybszy sposób tooretrieve pojedyncza jednostka z usługi tabeli hello.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Zastępowanie jednostki
tooreplace jednostki, pobrać hello usługi tabel, zmodyfikuj obiekt jednostki hello i następnie zapisz zmiany hello ponownie toohello usługi tabel. Witaj poniższy kod zmienia istniejący klient telefonu i adresu e-mail. Zamiast wywoływać metodę **table_operation::insert_entity**, ten kod używa **table_operation::replace_entity**. Powoduje to toobe jednostki hello całkowicie zastąpiona na powitania serwera, chyba że hello jednostki na powitania serwera została zmieniona, ponieważ został on pobrany, w którym to przypadku hello operacja zakończy się niepowodzeniem. Ten błąd jest tooprevent aplikacji nieodwracalne nadpisanie zmiany wprowadzone od hello pobierania i aktualizowania przez inny składnik aplikacji. Hello prawidłowego obsługi tego błędu jest jednostki hello tooretrieve ponownie, wprowadź żądane zmiany (jeśli jest nadal ważny), a następnie wykonaj inną **table_operation::replace_entity** operacji. Witaj w następnej sekcji opisano, jak toooverride to zachowanie.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Wstawianie lub zastępowanie jednostki
**table_operation::replace_entity** operacji zakończy się niepowodzeniem, jeśli jednostka hello została zmieniona, ponieważ został on pobrany z serwera hello. Ponadto należy pobrać hello jednostki z powitania serwera najpierw **table_operation::replace_entity** toobe powiodło się. Czasami jednak nie wiesz, jeśli hello jednostka istnieje na serwerze hello i hello bieżące wartości znajdujące się w niej nie mają znaczenia — aktualizacja powinna nadpisać je wszystkie. tooaccomplish, należy użyć **table_operation::insert_or_replace_entity** operacji. Ta operacja wstawi hello jednostki, jeśli nie istnieje, lub zastąpi ją, jeśli tak jest, niezależnie od tego, kiedy dokonano hello ostatniej aktualizacji. W hello poniższy przykład kodu, hello jednostka klienta dla Jan Kowalski nadal jest pobierana, ale następnie jest zapisywana serwera zapasowego toohello za pośrednictwem **table_operation::insert_or_replace_entity**. Wszelkie aktualizacje wprowadzone jednostki toohello między hello operacji pobierania i aktualizacji zostaną zastąpione.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Tworzenie zapytania do podzbioru właściwości jednostki
Tabela tooa kwerend może pobrać kilka właściwości jednostki. Witaj zapytanie w hello następującego kodu używa hello **table_query::set_select_columns** metody tooreturn tylko hello adresy e-mail jednostek w tabeli hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Badania kilka właściwości jednostki jest operacją bardziej efektywne niż pobierania wszystkich właściwości.
> 
> 

## <a name="delete-an-entity"></a>Usuwanie jednostki
Po jej pobraniu można z łatwością usunąć jednostkę. Po pobraniu jednostki hello wywołać **table_operation::delete_entity** z hello toodelete jednostki. Następnie wywołaj hello **cloud_table.execute** metody. Witaj poniższy kod pobiera i usunięcie jednostki z kluczem partycji "Smith" i kluczem wiersza "Jeff".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Usuwanie tabeli
Na koniec hello poniższy przykład kodu usuwa tabelę z konta magazynu. Tabela, która została usunięta będzie niedostępna toobe ponownie utworzone w danym okresie czasu po usunięciu hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu tabel hello, wykonaj te toolearn łącza więcej informacji na temat usługi Azure Storage:  

* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Jak toouse magazynu obiektów Blob w języku C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Jak toouse magazynu kolejek w języku C++](storage-c-plus-plus-how-to-use-queues.md)
* [Lista zasobów magazynu Azure w języku C++](storage-c-plus-plus-enumeration.md)
* [Biblioteka klienta usługi Storage for C++ — dokumentacja](http://azure.github.io/azure-storage-cpp)
* [Dokumentację magazynu platformy Azure](https://azure.microsoft.com/documentation/services/storage/)
