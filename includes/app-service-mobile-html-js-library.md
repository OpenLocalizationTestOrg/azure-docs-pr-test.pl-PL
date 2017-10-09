## <a name="create-client"></a>Tworzenie połączenia klienta
Utwórz połączenie klienta, tworząc obiekt `WindowsAzure.MobileServiceClient`.  Zastąp `appUrl` z tooyour adres URL aplikacji mobilnej.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Praca z tabelami
dane tooaccess lub aktualizacji, tworzy tabelę odwołania toohello wewnętrznej bazy danych. Zastąp `tableName` o nazwie hello tabeli

```
var table = client.getTable(tableName);
```

Po utworzeniu odwołania do tabeli możesz kontynuować pracę z tabelą:

* [Odpytywanie tabeli](#querying)
  * [Filtrowanie danych](#table-filter)
  * [Stronicowanie danych](#table-paging)
  * [Sortowanie danych](#sorting-data)
* [Wstawianie danych](#inserting)
* [Modyfikowanie danych](#modifying)
* [Usuwanie danych](#deleting)

### <a name="querying"></a>Instrukcje: odpytywanie odwołania do tabeli
Po utworzeniu odwołania do tabeli, można go tooquery danych na powitania serwera.  Zapytania są tworzone w języku przypominającym LINQ.
tooreturn wszystkich danych z tabeli hello, hello Użyj następującego kodu:

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

Funkcja Powodzenie Hello jest wywoływana z wynikami hello.  Nie używaj `for (var i in results)` w Powodzenie hello działać zgodnie z którego będzie iteracja informacje zawarte w wynikach hello gdy inne funkcje zapytań (takie jak `.includeTotalCount()`) są używane.

Aby uzyskać więcej informacji na powitania składnia zapytania, zobacz hello [obiektu dokumentację dotyczącą zapytań].

#### <a name="table-filter"></a>Filtrowanie danych na powitania serwera
Można użyć `where` klauzuli hello w odwołaniu do tabeli:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Można także użyć funkcji filtrujące hello obiektu.  W takim przypadku hello `this` zmienna jest przypisana toothe bieżący obiekt, którego jest wykonywane filtrowanie.  Hello następującego kodu jest wcześniejsze przykład toohello taką samą funkcję:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Stronicowanie danych
Korzystanie z hello `take()` i `skip()` metody.  Na przykład, jeśli chcesz toosplit hello tabeli do wiersza 100 rekordów:

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

Witaj `.includeTotalCount()` metoda jest używane tooadd obiektu totalCount pola toohello wyników.  W polu totalCount jest wypełniony hello całkowita liczba rekordów, które będzie zwracany, jeśli Stronicowanie nie jest używany.

Następnie można użyć zmiennej strony hello i niektóre tooprovide przyciski interfejsu użytkownika strony listy; Użyj `loadPage()` załadować hello nowych rekordów dla każdej strony.  Implementuje buforowanie toospeed toorecords dostępu, które zostały już załadowane.

#### <a name="sorting-data"></a>Instrukcje: zwracanie posortowanych danych
Użyj hello `.orderBy()` lub `.orderByDescending()` metod zapytania:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Aby uzyskać więcej informacji na powitania obiektu zapytania, zobacz hello [obiektu dokumentację dotyczącą zapytań].

### <a name="inserting"></a>Instrukcje: wstawianie danych
Utwórz obiekt JavaScript z odpowiednią datą hello i wywołanie `table.insert()` asynchronicznie:

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

Na pomyślne wstawiania hello wstawiony element jest zwracany za hello dodatkowe pola, które są wymagane dla operacji synchronizacji.  Zaktualizuj własną pamięć podręczną o te informacje na potrzeby późniejszych aktualizacji.

Hello Azure Mobile Apps Node.js Server SDK obsługuje schematu dynamicznego do celów programistycznych.  Dynamiczne schematu umożliwia tooadd kolumn toohello tabeli, określając je w operacji insert lub update.  Zaleca się wyłączenie schematu dynamicznego przed przeniesieniem tooproduction Twojej aplikacji.

### <a name="modifying"></a>Instrukcje: modyfikowanie danych
Podobne toohello `.insert()` metody, należy utworzyć obiekt aktualizacji i wywoływać `.update()`.  Hello obiektu update musi zawierać identyfikator hello hello toobe rekordów zaktualizowane — identyfikator hello są uzyskiwane podczas odczytywania rekordu hello lub podczas wywoływania metody `.insert()`.

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a>Instrukcje: usuwanie danych
toodelete rekordu, wywołanie hello `.del()` metody.  Podaj identyfikator hello odwołanie do obiektu:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
