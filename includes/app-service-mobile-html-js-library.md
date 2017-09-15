## <span data-ttu-id="3c885-101"><a name="create-client"></a>Tworzenie połączenia klienta</span><span class="sxs-lookup"><span data-stu-id="3c885-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="3c885-102">Utwórz połączenie klienta, tworząc obiekt `WindowsAzure.MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="3c885-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="3c885-103">Zastąp ciąg `appUrl` adresem URL Twojej aplikacji Mobile App.</span><span class="sxs-lookup"><span data-stu-id="3c885-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="3c885-104"><a name="table-reference"></a>Praca z tabelami</span><span class="sxs-lookup"><span data-stu-id="3c885-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="3c885-105">Aby uzyskać dostęp do danych lub je zaktualizować, utwórz odwołanie do tabeli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="3c885-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="3c885-106">Zastąp ciąg `tableName` nazwą tabeli</span><span class="sxs-lookup"><span data-stu-id="3c885-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="3c885-107">Po utworzeniu odwołania do tabeli możesz kontynuować pracę z tabelą:</span><span class="sxs-lookup"><span data-stu-id="3c885-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="3c885-108">Odpytywanie tabeli</span><span class="sxs-lookup"><span data-stu-id="3c885-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="3c885-109">Filtrowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="3c885-110">Stronicowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="3c885-111">Sortowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="3c885-112">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="3c885-113">Modyfikowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="3c885-114">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="3c885-115"><a name="querying"></a>Instrukcje: odpytywanie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="3c885-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="3c885-116">Po utworzeniu odwołania do tabeli możesz przy jego użyciu wysłać zapytanie o dane na serwerze.</span><span class="sxs-lookup"><span data-stu-id="3c885-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="3c885-117">Zapytania są tworzone w języku przypominającym LINQ.</span><span class="sxs-lookup"><span data-stu-id="3c885-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="3c885-118">Aby zwrócić wszystkie dane z tabeli, użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="3c885-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="3c885-119">Funkcja success jest wywoływana z użyciem wyników.</span><span class="sxs-lookup"><span data-stu-id="3c885-119">The success function is called with the results.</span></span>  <span data-ttu-id="3c885-120">Nie umieszczaj w funkcji success pętli `for (var i in results)`, ponieważ będzie ona przechodzić przez informacje zawarte w wynikach w czasie, gdy będą używane inne funkcje zapytań (takie jak `.includeTotalCount()`).</span><span class="sxs-lookup"><span data-stu-id="3c885-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="3c885-121">Aby dowiedzieć się więcej o składni zapytań, zobacz [dokumentację obiektu Query].</span><span class="sxs-lookup"><span data-stu-id="3c885-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="3c885-122"><a name="table-filter"></a>Filtrowanie danych na serwerze</span><span class="sxs-lookup"><span data-stu-id="3c885-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="3c885-123">W przypadku odwołania do tabeli możesz użyć klauzuli `where`:</span><span class="sxs-lookup"><span data-stu-id="3c885-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="3c885-124">Ponadto możesz użyć funkcji filtrującej obiekt.</span><span class="sxs-lookup"><span data-stu-id="3c885-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="3c885-125">W tym przykładzie zmienna `this` jest przypisana do obecnie filtrowanego obiektu.</span><span class="sxs-lookup"><span data-stu-id="3c885-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="3c885-126">Poniższy kod jest funkcjonalnie równoważny z poprzednim przykładem:</span><span class="sxs-lookup"><span data-stu-id="3c885-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="3c885-127"><a name="table-paging"></a>Stronicowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="3c885-128">Skorzystaj z metod `take()` i `skip()`.</span><span class="sxs-lookup"><span data-stu-id="3c885-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="3c885-129">Na przykład jeśli chcesz podzielić tabelę na rekordy składające się ze 100 wierszy:</span><span class="sxs-lookup"><span data-stu-id="3c885-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
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

<span data-ttu-id="3c885-130">Metoda `.includeTotalCount()` powoduje dodanie pola totalCount do obiektu results.</span><span class="sxs-lookup"><span data-stu-id="3c885-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="3c885-131">Pole totalCount zostanie wypełnione łączną liczbą rekordów, które zostałyby zwrócone w przypadku braku stronicowania.</span><span class="sxs-lookup"><span data-stu-id="3c885-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="3c885-132">Następnie możesz udostępnić listę stron za pomocą zmiennej pages i przycisków interfejsu użytkownika. Aby załadować nowe rekordy na każdą stronę, użyj metody `loadPage()`.</span><span class="sxs-lookup"><span data-stu-id="3c885-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="3c885-133">Zaimplementuj buforowanie, aby przyspieszyć dostęp do już załadowanych rekordów.</span><span class="sxs-lookup"><span data-stu-id="3c885-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="3c885-134"><a name="sorting-data"></a>Instrukcje: zwracanie posortowanych danych</span><span class="sxs-lookup"><span data-stu-id="3c885-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="3c885-135">Użyj metody zapytania `.orderBy()` lub `.orderByDescending()`:</span><span class="sxs-lookup"><span data-stu-id="3c885-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="3c885-136">Aby uzyskać informacje o obiekcie Query, zobacz [dokumentację obiektu Query].</span><span class="sxs-lookup"><span data-stu-id="3c885-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="3c885-137"><a name="inserting"></a>Instrukcje: wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="3c885-138">Utwórz obiekt JavaScript z odpowiednimi danymi i asynchronicznie wywołaj metodę `table.insert()`:</span><span class="sxs-lookup"><span data-stu-id="3c885-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="3c885-139">Pomyślnie wstawiony element zostaje zwrócony z dodatkowymi polami, które są wymagane przez operacje synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="3c885-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="3c885-140">Zaktualizuj własną pamięć podręczną o te informacje na potrzeby późniejszych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3c885-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="3c885-141">Zestaw Azure Mobile Apps Node.js Server SDK obsługuje schemat dynamiczny dla celów deweloperskich.</span><span class="sxs-lookup"><span data-stu-id="3c885-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="3c885-142">Schemat dynamiczny umożliwia dodawanie kolumn do tabeli przez podanie ich w operacji wstawiania lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3c885-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="3c885-143">Zalecamy wyłączenie schematu dynamicznego przed przeniesieniem aplikacji na etap produkcji.</span><span class="sxs-lookup"><span data-stu-id="3c885-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="3c885-144"><a name="modifying"></a>Instrukcje: modyfikowanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="3c885-145">Podobnie jak w przypadku metody `.insert()` należy utworzyć obiekt aktualizacji, a następnie wywołać metodę `.update()`.</span><span class="sxs-lookup"><span data-stu-id="3c885-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="3c885-146">Obiekt aktualizacji musi zawierać identyfikator rekordu do zaktualizowania — identyfikator ten uzyskuje się podczas odczytu rekordu bądź wywoływania metody `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="3c885-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="3c885-147"><a name="deleting"></a>Instrukcje: usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="3c885-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="3c885-148">Aby usunąć rekord, wywołaj metodę `.del()`.</span><span class="sxs-lookup"><span data-stu-id="3c885-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="3c885-149">Przekaż identyfikator w odwołaniu do obiektu:</span><span class="sxs-lookup"><span data-stu-id="3c885-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
