---
title: Funkcje JSON bazy danych SQL platformy Azure | Dokumentacja firmy Microsoft
description: "Baza danych SQL Azure umożliwia analizy, zapytań i formatowanie danych w notacji języka JavaScript Object Notation (JSON)."
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="d424a-103">Wprowadzenie do korzystania z funkcji JSON w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d424a-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="d424a-104">Azure umożliwia bazy danych SQL, analizy i zapytania dane reprezentowane w notacji obiektu JavaScript [(JSON)](http://www.json.org/) sformatowanie i wyeksportuj dane relacyjne jako tekstu JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="d424a-105">JSON to format popularnych danych używane do wymiany danych w nowoczesnych witryn sieci web i aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="d424a-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="d424a-106">JSON jest również używane do przechowywania częściowo ustrukturyzowanych danych w plikach dziennika lub w bazach danych NoSQL, takie jak [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d424a-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="d424a-107">Wiele usług sieci web REST wyniki zwracane formatować jako tekstu JSON lub akceptować dane w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="d424a-108">Azure większość usług takich jak [usługi Azure Search](https://azure.microsoft.com/services/search/), [usługi Azure Storage](https://azure.microsoft.com/services/storage/), i [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/) mają punkty końcowe REST, które zwracają lub korzystać z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="d424a-109">Baza danych SQL Azure pozwala łatwo pracować z danych JSON i integrowania bazy danych z usługami nowoczesnych.</span><span class="sxs-lookup"><span data-stu-id="d424a-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="d424a-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d424a-110">Overview</span></span>
<span data-ttu-id="d424a-111">Baza danych SQL Azure udostępnia następujące funkcje do pracy z danymi JSON:</span><span class="sxs-lookup"><span data-stu-id="d424a-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![Funkcje JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="d424a-113">Jeśli masz tekst JSON można wyodrębnić dane z JSON lub sprawdzić, czy JSON jest prawidłowo sformatowane przy użyciu wbudowanych funkcji [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), i [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="d424a-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="d424a-114">[JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) funkcja pozwala zaktualizować wartość w tekście JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="d424a-115">Więcej zaawansowane zapytania i analizy, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) funkcji można przekształcić na tablicę obiektów JSON do zestawu wierszy.</span><span class="sxs-lookup"><span data-stu-id="d424a-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="d424a-116">Każde zapytanie SQL mogą być wykonywane na zestaw wyników zwrócony.</span><span class="sxs-lookup"><span data-stu-id="d424a-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="d424a-117">Na koniec istnieje [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) klauzuli, które umożliwia formatowanie danych przechowywane w tabelach relacyjne jako tekstu JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="d424a-118">Formatowanie danych relacyjnych w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="d424a-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="d424a-119">Jeśli masz usługi sieci web, że format pobiera dane z bazy danych warstwy i udostępnia odpowiedź w formacie JSON lub struktury języka JavaScript po stronie klienta lub bibliotek, które akceptują dane w formacie JSON zawartości bazy danych można sformatować jako JSON bezpośrednio w zapytaniu SQL.</span><span class="sxs-lookup"><span data-stu-id="d424a-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="d424a-120">Możesz już trzeba napisać kod aplikacji, które formatuje wyników z bazy danych SQL Azure w formacie JSON lub dodać niektóre Biblioteka serializacji JSON do przekonwertowania wyników zapytań tabelarycznych, a następnie serializacji obiektów do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="d424a-121">Zamiast tego można w klauzuli FOR JSON wyników zapytania SQL w formacie JSON w usłudze Azure SQL Database i używać go bezpośrednio w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d424a-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="d424a-122">W poniższym przykładzie wierszy z tabeli Sales.Customer formacie JSON przy użyciu klauzuli FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="d424a-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="d424a-123">Klauzula FOR JSON PATH formatuje wyniki zapytania jako tekst w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="d424a-124">Nazwy kolumn są używane jako klucze, gdy wartości komórek są generowane jako wartości JSON:</span><span class="sxs-lookup"><span data-stu-id="d424a-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="d424a-125">Zestaw wyników jest formatowana jako tablica JSON, w którym każdy wiersz jest formatowana jako oddzielny obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="d424a-126">ŚCIEŻKA wskazuje, że format wyjściowy wyniku JSON można dostosować za pomocą kropkowego w aliasów kolumn.</span><span class="sxs-lookup"><span data-stu-id="d424a-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="d424a-127">Następujące zapytanie powoduje zmianę klucza "CustomerName" w formacie JSON dane wyjściowe i umieszcza numer telefonu i faksu w obiekcie podrzędne "Skontaktuj się z":</span><span class="sxs-lookup"><span data-stu-id="d424a-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="d424a-128">Dane wyjściowe tego zapytania wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d424a-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="d424a-129">W tym przykładzie firma Microsoft zwracany pojedynczy obiekt JSON zamiast tablicy, określając [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opcji.</span><span class="sxs-lookup"><span data-stu-id="d424a-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="d424a-130">Można użyć tej opcji, jeśli wiadomo, że zwróconego pojedynczy obiekt wyniku zapytania.</span><span class="sxs-lookup"><span data-stu-id="d424a-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="d424a-131">Głównym wartość w klauzuli FOR JSON jest, że umożliwia zwracanie złożonych hierarchiczne dane z bazy danych w formacie zagnieżdżonych obiektów JSON lub tablicą.</span><span class="sxs-lookup"><span data-stu-id="d424a-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="d424a-132">Poniższy przykład przedstawia sposób Uwzględnij zamówienia, które należą do klienta jako tablica zagnieżdżona zleceń:</span><span class="sxs-lookup"><span data-stu-id="d424a-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="d424a-133">Zamiast wysyłać oddzielne kwerendy w celu uzyskania danych klienta, a następnie pobrać listę zleceń powiązane, można znaleźć wszystkie niezbędne dane z pojedynczego zapytania, jak pokazano w poniższych przykładowych danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="d424a-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="d424a-134">Praca z danymi w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="d424a-134">Working with JSON data</span></span>
<span data-ttu-id="d424a-135">Złożone obiekty podrzędne, tablic lub danymi hierarchicznymi braku ściśle strukturalnych danych lub rozwijać struktury danych użytkownika w czasie, w formacie JSON może pomóc do reprezentowania żadnej struktury danych złożonych.</span><span class="sxs-lookup"><span data-stu-id="d424a-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="d424a-136">JSON to tekstowy format, którego można używać innych typów ciągu w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d424a-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="d424a-137">Możesz wysłać lub przechowywać dane JSON jako standardowa NVARCHAR:</span><span class="sxs-lookup"><span data-stu-id="d424a-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="d424a-138">Dane JSON, w tym przykładzie odpowiada za pomocą typu NVARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="d424a-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="d424a-139">JSON można wstawiać do tej tabeli lub podana jako wartość argumentu procedury składowanej przy użyciu standardowej składni języka Transact-SQL, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d424a-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="d424a-140">Język klienta lub biblioteki, która współdziała z ciągu danych w bazie danych SQL Azure będzie również współpracować z danych JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="d424a-141">JSON mogą być przechowywane w dowolnej tabeli, która obsługuje typ NVARCHAR, takich jak zoptymalizowanych pod kątem pamięci tabeli lub tabeli z systemową kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="d424a-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="d424a-142">JSON nie zapewnia żadnych ograniczeń w kodzie po stronie klienta lub w warstwie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d424a-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="d424a-143">Wykonywanie zapytania na danych JSON</span><span class="sxs-lookup"><span data-stu-id="d424a-143">Querying JSON data</span></span>
<span data-ttu-id="d424a-144">Jeśli masz dane w formacie JSON przechowywane w tabelach Azure SQL, JSON funkcje umożliwiają używanie tych danych w dowolnym zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d424a-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="d424a-145">Funkcje JSON, które są dostępne w let bazy danych Azure SQL Traktuj dane w formacie JSON jako inny typ danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d424a-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="d424a-146">Możesz łatwo Wyodrębnij wartości w tekście JSON i użyć danych JSON w dowolnej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="d424a-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="d424a-147">Funkcja JSON_VALUE wyodrębnianie wartości w tekście JSON przechowywanych w kolumnie danych.</span><span class="sxs-lookup"><span data-stu-id="d424a-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="d424a-148">Funkcja ta używa ścieżki notacji języka JavaScript odwoływać się do wartości w tekście JSON do wyodrębnienia.</span><span class="sxs-lookup"><span data-stu-id="d424a-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="d424a-149">Wyodrębnionego wartość może być używana w dowolnej części zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d424a-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="d424a-150">Funkcja JSON_QUERY jest podobny do JSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="d424a-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="d424a-151">W odróżnieniu od JSON_VALUE ta funkcja wyodrębnia złożonych obiektu podrzędnego, takiego jak tablice lub obiektów, które są umieszczane w tekście JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="d424a-152">Funkcja JSON_MODIFY pozwala określić ścieżkę do wartości w tekście JSON, który powinien zostać zaktualizowany, a także nową wartość, która zastąpi stare hasło.</span><span class="sxs-lookup"><span data-stu-id="d424a-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="d424a-153">Dzięki temu można łatwo aktualizować tekst JSON bez ponownej analizy całego struktury.</span><span class="sxs-lookup"><span data-stu-id="d424a-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="d424a-154">Ponieważ JSON są przechowywane w postaci zwykłego tekstu, nie ma żadnych gwarancji, że wartościami przechowywanymi w kolumnach tekstu są prawidłowo sformatowane.</span><span class="sxs-lookup"><span data-stu-id="d424a-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="d424a-155">Aby sprawdzić, czy tekst w formacie JSON przechowywane jest poprawnie sformatowana przy użyciu standardowych ograniczenia sprawdzania bazy danych SQL Azure i funkcja ISJSON:</span><span class="sxs-lookup"><span data-stu-id="d424a-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="d424a-156">Jeśli tekst wejściowy jest poprawnie sformatowana JSON, funkcja ISJSON zwraca wartość 1.</span><span class="sxs-lookup"><span data-stu-id="d424a-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="d424a-157">Na każdym insert lub update kolumny JSON to ograniczenie zweryfikuje, że nowe wartości tekstowej nie jest nieprawidłowo sformatowany kod JSON.</span><span class="sxs-lookup"><span data-stu-id="d424a-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="d424a-158">Przekształcania JSON w formacie tabelarycznym</span><span class="sxs-lookup"><span data-stu-id="d424a-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="d424a-159">Baza danych SQL Azure umożliwia również przekształcenie kolekcji JSON do danych JSON format i obciążenia lub zapytań tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="d424a-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="d424a-160">OPENJSON to funkcja wartościami przechowywanymi w tabeli, która analizuje tekst JSON, lokalizuje jest Tablica obiektów JSON iterację elementów tablicy i zwraca jeden wiersz w wyniku danych wyjściowych dla każdego elementu tablicy.</span><span class="sxs-lookup"><span data-stu-id="d424a-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![Tabelaryczne JSON](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="d424a-162">W powyższym przykładzie można określić gdzie umieścić tablicy JSON, który powinien zostać otwarty (w $. Ścieżka zamówienia), które kolumny ma zostać zwrócony jako wynik i gdzie można znaleźć wartości JSON, które zostaną zwrócone jako komórki.</span><span class="sxs-lookup"><span data-stu-id="d424a-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="d424a-163">Firma Microsoft można przekształcać tablica JSON w @orders zmienną do zestawu wierszy, analizować ten zestaw wyników lub wstawić wierszy do tabeli standardowe:</span><span class="sxs-lookup"><span data-stu-id="d424a-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="d424a-164">Kolekcja zamówień formatowane jako tablica JSON i podać jako parametr do procedury składowanej można analizować i wstawione do tabeli zamówienia.</span><span class="sxs-lookup"><span data-stu-id="d424a-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d424a-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d424a-165">Next steps</span></span>
<span data-ttu-id="d424a-166">Aby dowiedzieć się, jak zintegrować JSON aplikacji, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="d424a-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="d424a-167">TechNet Blog</span><span class="sxs-lookup"><span data-stu-id="d424a-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="d424a-168">Dokumentacji MSDN</span><span class="sxs-lookup"><span data-stu-id="d424a-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="d424a-169">Channel 9 wideo</span><span class="sxs-lookup"><span data-stu-id="d424a-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="d424a-170">Informacje na temat różnych scenariuszy integracji JSON do aplikacji, zobacz pokazy w tym [wideo z witryny Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) lub znaleźć scenariusz, który jest zgodny z zastosowaniem w [ogłoszeń blogu JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="d424a-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

