## <span data-ttu-id="efb9a-101"><a name="create-client"></a>Tworzenie połączenia klienta</span><span class="sxs-lookup"><span data-stu-id="efb9a-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="efb9a-102">Utwórz połączenie klienta, tworząc obiekt `WindowsAzure.MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="efb9a-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="efb9a-103">Zastąp `appUrl` z tooyour adres URL aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="efb9a-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="efb9a-104"><a name="table-reference"></a>Praca z tabelami</span><span class="sxs-lookup"><span data-stu-id="efb9a-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="efb9a-105">dane tooaccess lub aktualizacji, tworzy tabelę odwołania toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="efb9a-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="efb9a-106">Zastąp `tableName` o nazwie hello tabeli</span><span class="sxs-lookup"><span data-stu-id="efb9a-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="efb9a-107">Po utworzeniu odwołania do tabeli możesz kontynuować pracę z tabelą:</span><span class="sxs-lookup"><span data-stu-id="efb9a-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="efb9a-108">Odpytywanie tabeli</span><span class="sxs-lookup"><span data-stu-id="efb9a-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="efb9a-109">Filtrowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="efb9a-110">Stronicowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="efb9a-111">Sortowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="efb9a-112">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="efb9a-113">Modyfikowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="efb9a-114">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="efb9a-115"><a name="querying"></a>Instrukcje: odpytywanie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="efb9a-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="efb9a-116">Po utworzeniu odwołania do tabeli, można go tooquery danych na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="efb9a-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="efb9a-117">Zapytania są tworzone w języku przypominającym LINQ.</span><span class="sxs-lookup"><span data-stu-id="efb9a-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="efb9a-118">tooreturn wszystkich danych z tabeli hello, hello Użyj następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="efb9a-118">tooreturn all data from hello table, use hello following code:</span></span>

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

<span data-ttu-id="efb9a-119">Funkcja Powodzenie Hello jest wywoływana z wynikami hello.</span><span class="sxs-lookup"><span data-stu-id="efb9a-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="efb9a-120">Nie używaj `for (var i in results)` w Powodzenie hello działać zgodnie z którego będzie iteracja informacje zawarte w wynikach hello gdy inne funkcje zapytań (takie jak `.includeTotalCount()`) są używane.</span><span class="sxs-lookup"><span data-stu-id="efb9a-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="efb9a-121">Aby uzyskać więcej informacji na powitania składnia zapytania, zobacz hello [obiektu dokumentację dotyczącą zapytań].</span><span class="sxs-lookup"><span data-stu-id="efb9a-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="efb9a-122"><a name="table-filter"></a>Filtrowanie danych na powitania serwera</span><span class="sxs-lookup"><span data-stu-id="efb9a-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="efb9a-123">Można użyć `where` klauzuli hello w odwołaniu do tabeli:</span><span class="sxs-lookup"><span data-stu-id="efb9a-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="efb9a-124">Można także użyć funkcji filtrujące hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="efb9a-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="efb9a-125">W takim przypadku hello `this` zmienna jest przypisana toothe bieżący obiekt, którego jest wykonywane filtrowanie.</span><span class="sxs-lookup"><span data-stu-id="efb9a-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="efb9a-126">Hello następującego kodu jest wcześniejsze przykład toohello taką samą funkcję:</span><span class="sxs-lookup"><span data-stu-id="efb9a-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="efb9a-127"><a name="table-paging"></a>Stronicowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="efb9a-128">Korzystanie z hello `take()` i `skip()` metody.</span><span class="sxs-lookup"><span data-stu-id="efb9a-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="efb9a-129">Na przykład, jeśli chcesz toosplit hello tabeli do wiersza 100 rekordów:</span><span class="sxs-lookup"><span data-stu-id="efb9a-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

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

<span data-ttu-id="efb9a-130">Witaj `.includeTotalCount()` metoda jest używane tooadd obiektu totalCount pola toohello wyników.</span><span class="sxs-lookup"><span data-stu-id="efb9a-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="efb9a-131">W polu totalCount jest wypełniony hello całkowita liczba rekordów, które będzie zwracany, jeśli Stronicowanie nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="efb9a-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="efb9a-132">Następnie można użyć zmiennej strony hello i niektóre tooprovide przyciski interfejsu użytkownika strony listy; Użyj `loadPage()` załadować hello nowych rekordów dla każdej strony.</span><span class="sxs-lookup"><span data-stu-id="efb9a-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="efb9a-133">Implementuje buforowanie toospeed toorecords dostępu, które zostały już załadowane.</span><span class="sxs-lookup"><span data-stu-id="efb9a-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="efb9a-134"><a name="sorting-data"></a>Instrukcje: zwracanie posortowanych danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="efb9a-135">Użyj hello `.orderBy()` lub `.orderByDescending()` metod zapytania:</span><span class="sxs-lookup"><span data-stu-id="efb9a-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="efb9a-136">Aby uzyskać więcej informacji na powitania obiektu zapytania, zobacz hello [obiektu dokumentację dotyczącą zapytań].</span><span class="sxs-lookup"><span data-stu-id="efb9a-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="efb9a-137"><a name="inserting"></a>Instrukcje: wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="efb9a-138">Utwórz obiekt JavaScript z odpowiednią datą hello i wywołanie `table.insert()` asynchronicznie:</span><span class="sxs-lookup"><span data-stu-id="efb9a-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="efb9a-139">Na pomyślne wstawiania hello wstawiony element jest zwracany za hello dodatkowe pola, które są wymagane dla operacji synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="efb9a-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="efb9a-140">Zaktualizuj własną pamięć podręczną o te informacje na potrzeby późniejszych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="efb9a-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="efb9a-141">Hello Azure Mobile Apps Node.js Server SDK obsługuje schematu dynamicznego do celów programistycznych.</span><span class="sxs-lookup"><span data-stu-id="efb9a-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="efb9a-142">Dynamiczne schematu umożliwia tooadd kolumn toohello tabeli, określając je w operacji insert lub update.</span><span class="sxs-lookup"><span data-stu-id="efb9a-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="efb9a-143">Zaleca się wyłączenie schematu dynamicznego przed przeniesieniem tooproduction Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="efb9a-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="efb9a-144"><a name="modifying"></a>Instrukcje: modyfikowanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="efb9a-145">Podobne toohello `.insert()` metody, należy utworzyć obiekt aktualizacji i wywoływać `.update()`.</span><span class="sxs-lookup"><span data-stu-id="efb9a-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="efb9a-146">Hello obiektu update musi zawierać identyfikator hello hello toobe rekordów zaktualizowane — identyfikator hello są uzyskiwane podczas odczytywania rekordu hello lub podczas wywoływania metody `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="efb9a-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="efb9a-147"><a name="deleting"></a>Instrukcje: usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="efb9a-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="efb9a-148">toodelete rekordu, wywołanie hello `.del()` metody.</span><span class="sxs-lookup"><span data-stu-id="efb9a-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="efb9a-149">Podaj identyfikator hello odwołanie do obiektu:</span><span class="sxs-lookup"><span data-stu-id="efb9a-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
