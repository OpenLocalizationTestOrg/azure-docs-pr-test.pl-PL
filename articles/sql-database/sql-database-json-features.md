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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Wprowadzenie do korzystania z funkcji JSON w bazie danych SQL Azure
Azure umożliwia bazy danych SQL, analizy i zapytania dane reprezentowane w notacji obiektu JavaScript [(JSON)](http://www.json.org/) sformatowanie i wyeksportuj dane relacyjne jako tekstu JSON.

JSON to format popularnych danych używane do wymiany danych w nowoczesnych witryn sieci web i aplikacji dla urządzeń przenośnych. JSON jest również używane do przechowywania częściowo ustrukturyzowanych danych w plikach dziennika lub w bazach danych NoSQL, takie jak [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/). Wiele usług sieci web REST wyniki zwracane formatować jako tekstu JSON lub akceptować dane w formacie JSON. Azure większość usług takich jak [usługi Azure Search](https://azure.microsoft.com/services/search/), [usługi Azure Storage](https://azure.microsoft.com/services/storage/), i [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/) mają punkty końcowe REST, które zwracają lub korzystać z formatu JSON.

Baza danych SQL Azure pozwala łatwo pracować z danych JSON i integrowania bazy danych z usługami nowoczesnych.

## <a name="overview"></a>Omówienie
Baza danych SQL Azure zapewnia następujące funkcje do pracy z danymi JSON hello:

![Funkcje JSON](./media/sql-database-json-features/image_1.png)

Jeśli masz tekst JSON można wyodrębnić dane z JSON lub sprawdź, czy JSON jest prawidłowo sformatowany za pomocą funkcji wbudowanych hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), i [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Witaj [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) funkcja pozwala zaktualizować wartość w tekście JSON. Więcej zaawansowane zapytania i analizy, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) funkcji można przekształcić na tablicę obiektów JSON do zestawu wierszy. Każde zapytanie SQL mogą być wykonywane na powitania zwrócił zestaw wyników. Na koniec istnieje [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) klauzuli, które umożliwia formatowanie danych przechowywane w tabelach relacyjne jako tekstu JSON.

## <a name="formatting-relational-data-in-json-format"></a>Formatowanie danych relacyjnych w formacie JSON
Jeśli masz usługi sieci web, że format pobiera dane z bazy danych hello warstwy i udostępnia odpowiedź w formacie JSON lub struktury języka JavaScript po stronie klienta lub bibliotek, które akceptują dane w formacie JSON zawartości bazy danych można sformatować jako JSON bezpośrednio w zapytaniu SQL. Nie masz toowrite kodu aplikacji, które formatuje wyników z bazy danych SQL Azure w postaci JSON, lub Dołącz wyniki niektórych JSON serializacji biblioteki tooconvert zapytanie tabelaryczne i następnie serializować obiektów tooJSON format. Można użyć hello uzyskania wyników kwerendy SQL tooformat klauzuli JSON jako JSON w usłudze Azure SQL Database i użyj go bezpośrednio w aplikacji.

W hello poniższy przykład wiersze z tabeli Sales.Customer hello są sformatowane jako JSON za pomocą klauzuli FOR JSON hello:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

Klauzula FOR JSON PATH Hello formatuje hello wyniki zapytania hello jako tekstu JSON. Nazwy kolumn są używane jako klucze, gdy wartości komórek hello są generowane jako wartości JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

zestaw wyników Hello jest formatowana jako tablica JSON, w którym każdy wiersz jest formatowana jako oddzielny obiekt JSON.

ŚCIEŻKA wskazuje, że możesz dostosować hello format wyjściowy wyniku JSON przy użyciu kropkowego w aliasów kolumn. następujące zapytanie Hello zmienia nazwę hello klucza "CustomerName" hello, w formacie JSON dane wyjściowe hello i umieszcza numer telefonu i faksu w obiektu podrzędnego "Kontaktu" hello:

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

dane wyjściowe Hello to zapytanie wygląda następująco:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

W tym przykładzie firma Microsoft zwracany pojedynczy obiekt JSON zamiast tablicy, określając hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opcji. Można użyć tej opcji, jeśli wiadomo, że zwróconego pojedynczy obiekt wyniku zapytania.

Hello głównego wartość hello klauzuli FOR JSON jest, że umożliwia zwracanie złożonych hierarchiczne dane z bazy danych w formacie zagnieżdżonych obiektów JSON lub tablicą. powitania po przykładzie pokazano sposób porządkuje tooinclude, należące toohello klienta jako tablica zagnieżdżona zleceń:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Zamiast wysyłać dane klienta tooget oddzielne zapytania, a następnie toofetch listę zleceń powiązane, można uzyskać wszystkie hello niezbędne dane z pojedynczego zapytania, jak pokazano w hello następujące przykładowe dane wyjściowe:

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

## <a name="working-with-json-data"></a>Praca z danymi w formacie JSON
Jeśli nie masz ściśle strukturalnych danych w przypadku złożonych obiektów podrzędnych, tablic lub hierarchiczne dane, lub jeśli rozwijać struktury danych użytkownika w czasie, hello JSON format pomagają toorepresent żadnej struktury danych złożonych.

JSON to tekstowy format, którego można używać innych typów ciągu w bazie danych SQL Azure. Możesz wysłać lub przechowywać dane JSON jako standardowa NVARCHAR:

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

Witaj w tym przykładzie dane JSON jest reprezentowana przez przy użyciu typu NVARCHAR(MAX) hello. JSON można wstawiać do tej tabeli lub podana jako wartość argumentu procedury hello przechowywane przy użyciu standardowej składni języka Transact-SQL, jak pokazano w hello poniższy przykład:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Język klienta lub biblioteki, która współdziała z ciągu danych w bazie danych SQL Azure będzie również współpracować z danych JSON. JSON mogą być przechowywane w dowolnej tabeli, która obsługuje typ NVARCHAR hello, takich jak zoptymalizowanych pod kątem pamięci tabeli lub tabeli z systemową kontrolą wersji. JSON nie zapewnia żadnych ograniczenia w kodzie po stronie klienta hello lub hello warstwy bazy danych.

## <a name="querying-json-data"></a>Wykonywanie zapytania na danych JSON
Jeśli masz dane w formacie JSON przechowywane w tabelach Azure SQL, JSON funkcje umożliwiają używanie tych danych w dowolnym zapytania SQL.

Funkcje JSON, które są dostępne w let bazy danych Azure SQL Traktuj dane w formacie JSON jako inny typ danych SQL. Możesz łatwo wyodrębniania wartości z hello tekst JSON i użyć dane JSON w dowolnej kwerendy:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Funkcja JSON_VALUE Hello wyodrębnianie wartości w tekście JSON przechowywanych w kolumnie danych hello. Ta funkcja używa tooreference ścieżka notacji języka JavaScript wartość tooextract tekst JSON. wartość Hello wyodrębnione może być używana w dowolnej części zapytania SQL.

Funkcja JSON_QUERY Hello jest tooJSON_VALUE podobne. W odróżnieniu od JSON_VALUE ta funkcja wyodrębnia złożonych obiektu podrzędnego, takiego jak tablice lub obiektów, które są umieszczane w tekście JSON.

Funkcja JSON_MODIFY Hello pozwala określić ścieżkę hello wartości hello w hello tekst JSON, który powinien zostać zaktualizowany, a także nową wartość, która spowoduje zastąpienie hello stare hasło. Dzięki temu można łatwo aktualizować tekst JSON bez ponownej analizy hello całą strukturę.

Ponieważ JSON są przechowywane w postaci zwykłego tekstu, nie ma żadnych gwarancji, że hello wartościami przechowywanymi w tekst kolumny są poprawnie sformatowana. Można sprawdzić, czy tekst w formacie JSON przechowywane jest poprawnie sformatowana przy użyciu standardowych ograniczenia sprawdzania bazy danych SQL Azure i hello ISJSON funkcji:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Jeśli tekst wejściowy hello jest poprawnie sformatowana JSON, hello ISJSON funkcja zwraca wartość hello 1. Na każdym insert lub update kolumny JSON to ograniczenie zweryfikuje, że nowe wartości tekstowej nie jest nieprawidłowo sformatowany kod JSON.

## <a name="transforming-json-into-tabular-format"></a>Przekształcania JSON w formacie tabelarycznym
Baza danych SQL Azure umożliwia również przekształcenie kolekcji JSON do danych JSON format i obciążenia lub zapytań tabelarycznych.

OPENJSON to funkcja wartościami przechowywanymi w tabeli, która analizuje tekst JSON, lokalizuje jest Tablica obiektów JSON iteruje hello elementy tablicy hello i zwraca jeden wiersz w wyniku dane wyjściowe powitania dla każdego elementu tablicy hello.

![Tabelaryczne JSON](./media/sql-database-json-features/image_2.png)

W powyższym przykładzie hello można określić gdzie toolocate hello tablicy JSON, który powinien zostać otwarty (w hello $. Ścieżka zamówienia), które kolumny ma zostać zwrócony jako wynik, a w przypadku, gdy toofind hello wartości JSON, które zostaną zwrócone jako komórki.

Firma Microsoft można przekształcać tablica JSON w hello @orders zmienną do zestawu wierszy, analizować ten zestaw wyników lub wstawić wierszy do tabeli standardowe:

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
Kolekcja Hello zamówień formatowane jako tablica JSON i podać jako parametr procedury przechowywane toohello można przeanalizować i wstawione do tabeli zamówienia hello.

## <a name="next-steps"></a>Następne kroki
toolearn jak toointegrate JSON do aplikacji, zapoznaj się z tymi zasobami:

* [TechNet Blog](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Dokumentacji MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Channel 9 wideo](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn o różnych scenariuszy integracji JSON do aplikacji, zobacz pokazy hello na tym [wideo z witryny Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) lub znaleźć scenariusz, który jest zgodny z zastosowaniem w [ogłoszeń blogu JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

