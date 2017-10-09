---
title: Funkcje bazy danych SQL w formacie JSON aaaAzure | Dokumentacja firmy Microsoft
description: "Baza danych SQL Azure umożliwia tooparse, zapytań i formatowanie danych w notacji języka JavaScript Object Notation (JSON)."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="461ef-103">Wprowadzenie do korzystania z funkcji JSON w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="461ef-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="461ef-104">Azure umożliwia bazy danych SQL, analizy i zapytania dane reprezentowane w notacji obiektu JavaScript [(JSON)](http://www.json.org/) sformatowanie i wyeksportuj dane relacyjne jako tekstu JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="461ef-105">JSON to format popularnych danych używane do wymiany danych w nowoczesnych witryn sieci web i aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="461ef-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="461ef-106">JSON jest również używane do przechowywania częściowo ustrukturyzowanych danych w plikach dziennika lub w bazach danych NoSQL, takie jak [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="461ef-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="461ef-107">Wiele usług sieci web REST wyniki zwracane formatować jako tekstu JSON lub akceptować dane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="461ef-108">Azure większość usług takich jak [usługi Azure Search](https://azure.microsoft.com/services/search/), [usługi Azure Storage](https://azure.microsoft.com/services/storage/), i [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/) mają punkty końcowe REST, które zwracają lub korzystać z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="461ef-109">Baza danych SQL Azure pozwala łatwo pracować z danych JSON i integrowania bazy danych z usługami nowoczesnych.</span><span class="sxs-lookup"><span data-stu-id="461ef-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="461ef-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="461ef-110">Overview</span></span>
<span data-ttu-id="461ef-111">Baza danych SQL Azure zapewnia następujące funkcje do pracy z danymi JSON hello:</span><span class="sxs-lookup"><span data-stu-id="461ef-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Funkcje JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="461ef-113">Jeśli masz tekst JSON można wyodrębnić dane z JSON lub sprawdź, czy JSON jest prawidłowo sformatowany za pomocą funkcji wbudowanych hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), i [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="461ef-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="461ef-114">Witaj [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) funkcja pozwala zaktualizować wartość w tekście JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="461ef-115">Więcej zaawansowane zapytania i analizy, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) funkcji można przekształcić na tablicę obiektów JSON do zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="461ef-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="461ef-116">Każde zapytanie SQL mogą być wykonywane na powitania zwrócił zestaw wyników.</span><span class="sxs-lookup"><span data-stu-id="461ef-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="461ef-117">Na koniec istnieje [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) klauzuli, które umożliwia formatowanie danych przechowywane w tabelach relacyjne jako tekstu JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="461ef-118">Formatowanie danych relacyjnych w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="461ef-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="461ef-119">Jeśli masz usługi sieci web, że format pobiera dane z bazy danych hello warstwy i udostępnia odpowiedź w formacie JSON lub struktury języka JavaScript po stronie klienta lub bibliotek, które akceptują dane w formacie JSON zawartości bazy danych można sformatować jako JSON bezpośrednio w zapytaniu SQL.</span><span class="sxs-lookup"><span data-stu-id="461ef-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="461ef-120">Nie masz toowrite kodu aplikacji, które formatuje wyników z bazy danych SQL Azure w postaci JSON, lub Dołącz wyniki niektórych JSON serializacji biblioteki tooconvert zapytanie tabelaryczne i następnie serializować obiektów tooJSON format.</span><span class="sxs-lookup"><span data-stu-id="461ef-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="461ef-121">Można użyć hello uzyskania wyników kwerendy SQL tooformat klauzuli JSON jako JSON w usłudze Azure SQL Database i użyj go bezpośrednio w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="461ef-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="461ef-122">W hello poniższy przykład wiersze z tabeli Sales.Customer hello są sformatowane jako JSON za pomocą klauzuli FOR JSON hello:</span><span class="sxs-lookup"><span data-stu-id="461ef-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="461ef-123">Klauzula FOR JSON PATH Hello formatuje hello wyniki zapytania hello jako tekstu JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="461ef-124">Nazwy kolumn są używane jako klucze, gdy wartości komórek hello są generowane jako wartości JSON:</span><span class="sxs-lookup"><span data-stu-id="461ef-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="461ef-125">zestaw wyników Hello jest formatowana jako tablica JSON, w którym każdy wiersz jest formatowana jako oddzielny obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="461ef-126">ŚCIEŻKA wskazuje, że możesz dostosować hello format wyjściowy wyniku JSON przy użyciu kropkowego w aliasów kolumn.</span><span class="sxs-lookup"><span data-stu-id="461ef-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="461ef-127">następujące zapytanie Hello zmienia nazwę hello klucza "CustomerName" hello, w formacie JSON dane wyjściowe hello i umieszcza numer telefonu i faksu w obiektu podrzędnego "Kontaktu" hello:</span><span class="sxs-lookup"><span data-stu-id="461ef-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="461ef-128">dane wyjściowe Hello to zapytanie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="461ef-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="461ef-129">W tym przykładzie firma Microsoft zwracany pojedynczy obiekt JSON zamiast tablicy, określając hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opcji.</span><span class="sxs-lookup"><span data-stu-id="461ef-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="461ef-130">Można użyć tej opcji, jeśli wiadomo, że zwróconego pojedynczy obiekt wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="461ef-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="461ef-131">Hello głównego wartość hello klauzuli FOR JSON jest, że umożliwia zwracanie złożonych hierarchiczne dane z bazy danych w formacie zagnieżdżonych obiektów JSON lub tablicą.</span><span class="sxs-lookup"><span data-stu-id="461ef-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="461ef-132">powitania po przykładzie pokazano sposób porządkuje tooinclude, należące toohello klienta jako tablica zagnieżdżona zleceń:</span><span class="sxs-lookup"><span data-stu-id="461ef-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="461ef-133">Zamiast wysyłać dane klienta tooget oddzielne zapytania, a następnie toofetch listę zleceń powiązane, można uzyskać wszystkie hello niezbędne dane z pojedynczego zapytania, jak pokazano w hello następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="461ef-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="461ef-134">Praca z danymi w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="461ef-134">Working with JSON data</span></span>
<span data-ttu-id="461ef-135">Jeśli nie masz ściśle strukturalnych danych w przypadku złożonych obiektów podrzędnych, tablic lub hierarchiczne dane, lub jeśli rozwijać struktury danych użytkownika w czasie, hello JSON format pomagają toorepresent żadnej struktury danych złożonych.</span><span class="sxs-lookup"><span data-stu-id="461ef-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="461ef-136">JSON to tekstowy format, którego można używać innych typów ciągu w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="461ef-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="461ef-137">Możesz wysłać lub przechowywać dane JSON jako standardowa NVARCHAR:</span><span class="sxs-lookup"><span data-stu-id="461ef-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="461ef-138">Witaj w tym przykładzie dane JSON jest reprezentowana przez przy użyciu typu NVARCHAR(MAX) hello.</span><span class="sxs-lookup"><span data-stu-id="461ef-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="461ef-139">JSON można wstawiać do tej tabeli lub podana jako wartość argumentu procedury hello przechowywane przy użyciu standardowej składni języka Transact-SQL, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="461ef-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="461ef-140">Język klienta lub biblioteki, która współdziała z ciągu danych w bazie danych SQL Azure będzie również współpracować z danych JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="461ef-141">JSON mogą być przechowywane w dowolnej tabeli, która obsługuje typ NVARCHAR hello, takich jak zoptymalizowanych pod kątem pamięci tabeli lub tabeli z systemową kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="461ef-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="461ef-142">JSON nie zapewnia żadnych ograniczenia w kodzie po stronie klienta hello lub hello warstwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="461ef-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="461ef-143">Wykonywanie zapytania na danych JSON</span><span class="sxs-lookup"><span data-stu-id="461ef-143">Querying JSON data</span></span>
<span data-ttu-id="461ef-144">Jeśli masz dane w formacie JSON przechowywane w tabelach Azure SQL, JSON funkcje umożliwiają używanie tych danych w dowolnym zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="461ef-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="461ef-145">Funkcje JSON, które są dostępne w let bazy danych Azure SQL Traktuj dane w formacie JSON jako inny typ danych SQL.</span><span class="sxs-lookup"><span data-stu-id="461ef-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="461ef-146">Możesz łatwo wyodrębniania wartości z hello tekst JSON i użyć dane JSON w dowolnej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="461ef-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="461ef-147">Funkcja JSON_VALUE Hello wyodrębnianie wartości w tekście JSON przechowywanych w kolumnie danych hello.</span><span class="sxs-lookup"><span data-stu-id="461ef-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="461ef-148">Ta funkcja używa tooreference ścieżka notacji języka JavaScript wartość tooextract tekst JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="461ef-149">wartość Hello wyodrębnione może być używana w dowolnej części zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="461ef-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="461ef-150">Funkcja JSON_QUERY Hello jest tooJSON_VALUE podobne.</span><span class="sxs-lookup"><span data-stu-id="461ef-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="461ef-151">W odróżnieniu od JSON_VALUE ta funkcja wyodrębnia złożonych obiektu podrzędnego, takiego jak tablice lub obiektów, które są umieszczane w tekście JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="461ef-152">Funkcja JSON_MODIFY Hello pozwala określić ścieżkę hello wartości hello w hello tekst JSON, który powinien zostać zaktualizowany, a także nową wartość, która spowoduje zastąpienie hello stare hasło.</span><span class="sxs-lookup"><span data-stu-id="461ef-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="461ef-153">Dzięki temu można łatwo aktualizować tekst JSON bez ponownej analizy hello całą strukturę.</span><span class="sxs-lookup"><span data-stu-id="461ef-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="461ef-154">Ponieważ JSON są przechowywane w postaci zwykłego tekstu, nie ma żadnych gwarancji, że hello wartościami przechowywanymi w tekst kolumny są poprawnie sformatowana.</span><span class="sxs-lookup"><span data-stu-id="461ef-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="461ef-155">Można sprawdzić, czy tekst w formacie JSON przechowywane jest poprawnie sformatowana przy użyciu standardowych ograniczenia sprawdzania bazy danych SQL Azure i hello ISJSON funkcji:</span><span class="sxs-lookup"><span data-stu-id="461ef-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="461ef-156">Jeśli tekst wejściowy hello jest poprawnie sformatowana JSON, hello ISJSON funkcja zwraca wartość hello 1.</span><span class="sxs-lookup"><span data-stu-id="461ef-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="461ef-157">Na każdym insert lub update kolumny JSON to ograniczenie zweryfikuje, że nowe wartości tekstowej nie jest nieprawidłowo sformatowany kod JSON.</span><span class="sxs-lookup"><span data-stu-id="461ef-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="461ef-158">Przekształcania JSON w formacie tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="461ef-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="461ef-159">Baza danych SQL Azure umożliwia również przekształcenie kolekcji JSON do danych JSON format i obciążenia lub zapytań tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="461ef-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="461ef-160">OPENJSON to funkcja wartościami przechowywanymi w tabeli, która analizuje tekst JSON, lokalizuje jest Tablica obiektów JSON iteruje hello elementy tablicy hello i zwraca jeden wiersz w wyniku dane wyjściowe powitania dla każdego elementu tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="461ef-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![Tabelaryczne JSON](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="461ef-162">W powyższym przykładzie hello można określić gdzie toolocate hello tablicy JSON, który powinien zostać otwarty (w hello $. Ścieżka zamówienia), które kolumny ma zostać zwrócony jako wynik, a w przypadku, gdy toofind hello wartości JSON, które zostaną zwrócone jako komórki.</span><span class="sxs-lookup"><span data-stu-id="461ef-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="461ef-163">Firma Microsoft można przekształcać tablica JSON w hello @orders zmienną do zestawu wierszy, analizować ten zestaw wyników lub wstawić wierszy do tabeli standardowe:</span><span class="sxs-lookup"><span data-stu-id="461ef-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="461ef-164">Kolekcja Hello zamówień formatowane jako tablica JSON i podać jako parametr procedury przechowywane toohello można przeanalizować i wstawione do tabeli zamówienia hello.</span><span class="sxs-lookup"><span data-stu-id="461ef-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="461ef-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="461ef-165">Next steps</span></span>
<span data-ttu-id="461ef-166">toolearn jak toointegrate JSON do aplikacji, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="461ef-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="461ef-167">TechNet Blog</span><span class="sxs-lookup"><span data-stu-id="461ef-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="461ef-168">Dokumentacji MSDN</span><span class="sxs-lookup"><span data-stu-id="461ef-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="461ef-169">Channel 9 wideo</span><span class="sxs-lookup"><span data-stu-id="461ef-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="461ef-170">toolearn o różnych scenariuszy integracji JSON do aplikacji, zobacz pokazy hello na tym [wideo z witryny Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) lub znaleźć scenariusz, który jest zgodny z zastosowaniem w [ogłoszeń blogu JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="461ef-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

