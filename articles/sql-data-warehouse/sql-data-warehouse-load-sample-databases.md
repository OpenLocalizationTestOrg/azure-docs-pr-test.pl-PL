---
title: "aaaLoad przykładowych danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Ładowanie przykładowych danych do usługi SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>Ładowanie przykładowych danych do usługi SQL Data Warehouse
Wykonaj te tooload prostych kroków i bazy danych firmy Adventure Works próbki hello zapytania. Skrypty te należy najpierw użyć narzędzia sqlcmd toorun SQL, co spowoduje utworzenie tabel i widoków. Po utworzeniu tabel skrypty hello użyje bcp tooload danych.  Jeśli nie masz jeszcze sqlcmd i zainstalować narzędzia bcp, skorzystaj z poniższych linków za[zainstalować narzędzia bcp] [ install bcp] i zbyt[zainstalować narzędzia sqlcmd][install sqlcmd].

## <a name="load-sample-data"></a>Ładuj dane przykładowe
1. Pobierz hello [Adventure Works przykładowe skrypty dla usługi SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] pliku zip.
2. Wyodrębnij pliki hello z katalogu tooa zip pobranego na komputerze lokalnym.
3. Edytuj hello wyodrębniony plik aw_create.bat i ustaw następujące zmienne u góry pliku hello hello hello.  Można tooleave się nie spacji między hello "=" i hello parametru.  Poniżej przedstawiono przykłady może wyglądać dokonanych zmian.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. W wierszu polecenia systemu Windows uruchom aw_create.bat hello edytować.  Upewnij się, że znajdują się w katalogu hello, w którym zapisano aw_create.bat Twojego zmodyfikowaną wersję.
   Ten skrypt zostanie...
   
   * Upuść Adventure Works tabel ani widoków, które już istnieją w bazie danych
   * Utwórz hello Adventure Works tabele i widoki
   * Ładowanie każdej tabeli Adventure Works przy użyciu narzędzia bcp
   * Sprawdź poprawność hello liczb wierszy dla każdej tabeli Adventure Works
   * Zbieranie statystyk w każdej kolumnie dla każdej tabeli Adventure Works

## <a name="query-sample-data"></a>Dane przykładowe zapytania
Po przykładowych danych zostało załadowane do magazynu danych SQL, można szybko uruchomić kilka zapytań.  toorun kwerendy, połączenia bazy danych firmy Adventure Works tooyour nowo utworzonego w magazynie danych SQL Azure za pomocą programu Visual Studio i narzędzi SSDT, zgodnie z opisem w hello [zapytania z programem Visual Studio] [ query with Visual Studio] dokumentu.

Przykładem prostej wybierz tooget instrukcji wszystkie informacje hello hello pracowników:

```sql
SELECT * FROM DimEmployee;
```

Przykład bardziej złożonego zapytania używając konstrukcji, takich jak toolook GROUP BY w hello łączna kwota sprzedaży wszystkich każdego dnia:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Przykład SELECT z toofilter klauzuli WHERE, limit zamówień z przed określonej daty:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

Magazyn danych SQL obsługuje prawie wszystkie konstrukcje T-SQL, które obsługuje program SQL Server.  Różnice są udokumentowane w naszym [Migrowanie kodu] [ migrate code] dokumentacji.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy użytkownik miał tootry szansy kilka zapytań z przykładowymi danymi, sprawdź, jak za[opracowanie][develop], [załadować][load], lub [ Migrowanie] [ migrate] tooSQL hurtowni danych.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
