---
title: "aaaLoad danych z programu SQL Server do usługi Azure SQL Data Warehouse (bcp) | Dokumentacja firmy Microsoft"
description: "Rozmiar danych w małych używa bcp tooexport danych z plików tooflat programu SQL Server i zaimportuj dane hello bezpośrednio do usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Ładowanie danych z programu SQL Server do usługi Azure SQL Data Warehouse (pliki proste)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Dla małych zestawów danych można użyć hello bcp narzędzia wiersza polecenia tooexport danych z programu SQL Server i następnie ładowania ich bezpośrednio tooAzure SQL Data Warehouse.

W tym samouczku przy użyciu programu bcp zostaną wykonane następujące czynności:

* Eksportowanie tabeli z z programu SQL Server przy użyciu hello polecenia bcp out (lub tworzenie prostego pliku przykładowego)
* Tabela hello Import z pliku prostego tooSQL hurtowni danych.
* Tworzenie statystyk na powitania załadować danych.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Przed rozpoczęciem
### <a name="prerequisites"></a>Wymagania wstępne
toostep opisanych w tym samouczku, potrzebne są:

* Baza danych usługi SQL Data Warehouse
* Narzędzie wiersza polecenia bcp Hello zainstalowany
* narzędzia wiersza polecenia sqlcmd Hello zainstalowany

Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dane w formacie ASCII lub UTF-16
W przypadku tego samouczka z użyciem własnych danych, dane wymagają toouse hello ASCII lub kodowania UTF-16, ponieważ narzędzie bcp nie obsługuje UTF-8. 

Aparat PolyBase obsługuje format UTF-8, ale nie obsługuje jeszcze formatu UTF-16. Należy pamiętać, że jeśli bcp toocombine przy użyciu programu PolyBase konieczne będzie danych hello tootransform tooUTF-8 po ich wyeksportowaniu z programu SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Tworzenie tabeli docelowej
Zdefiniuj tabelę w magazynie danych SQL, która będzie tabelą docelową hello hello obciążenia. Witaj kolumn w tabeli hello musi odpowiadać toohello danych w poszczególnych wierszach pliku danych.

toocreate tabelę, otwórz wiersz polecenia i użyj hello toorun sqlcmd.exe następujące polecenie:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2. Tworzenie źródłowego pliku danych
Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt. Te dane są w formacie ASCII.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Opcjonalnie) tooexport dane z bazy danych programu SQL Server otwórz wiersz polecenia i uruchom następujące polecenie hello. Zastąp parametry TableName, ServerName, DatabaseName, Username i Password odpowiednimi informacjami.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Ładowanie danych hello
tooload hello danych, otwórz wiersz polecenia i uruchom hello następujące polecenie, zastępując hello wartości dla nazwy serwera, nazwę bazy danych, nazwę użytkownika i hasło z odpowiednimi informacjami.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Użyj tego polecenia tooverify hello dane zostały załadowane poprawnie

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Witaj wyniki powinny wyglądać następująco:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4. Tworzenie statystyk
Usługa SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk. tooget hello najlepszą wydajność zapytań, jest ważne toocreate statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub w danych powitania po każdej istotnej zmianie. Aby uzyskać szczegółowy opis statystyk, zobacz [statystyki][Statistics]. 

Witaj uruchom następujące polecenie toocreate statystyki dotyczące nowo załadowanej tabeli.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Eksportowanie danych z usługi SQL Data Warehouse
Dla zabawy możesz wyeksportować dane hello załadowane przed chwilą wstecz poza SQL Data Warehouse.  tooexport polecenia Hello jest hello dokładnie tak jak w przypadku eksportowania z programu SQL Server.

Istnieje jednak różnica w wynikach hello. Ponieważ hello dane są przechowywane w rozproszonych lokalizacjach w usłudze SQL Data Warehouse, podczas eksportowania danych każdy węzeł obliczeniowy zapisuje plik wyjściowy toohello danych. kolejność Hello hello danych w pliku wyjściowym hello jest prawdopodobnie inna niż kolejność hello hello danych w pliku wejściowym hello toobe.

### <a name="export-a-table-and-compare-exported-results"></a>Eksportowanie tabeli i porównywanie wyeksportowanych wyników
toosee hello wyeksportowane dane, otwórz wiersz polecenia i uruchom to polecenie z własnymi parametrami. ServerName jest nazwą powitania serwera logicznego SQL platformy Azure.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Możesz sprawdzić powitalne dane zostały poprawnie wyeksportowane, otwierając nowy plik hello. Witaj dane w pliku hello powinny odpowiadać tekstowi hello poniżej, ale prawdopodobnie będą posortowane w innej kolejności:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>Eksportowanie hello wyników zapytania
Można użyć hello **queryout** funkcja bcp tooexport hello wyniki zapytania, zamiast eksportować całą tabelę hello. 

## <a name="next-steps"></a>Następne kroki
Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].
Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].
Zobacz [omówienie tabeli] [ Table Overview] lub [składni polecenia CREATE TABLE] [ CREATE TABLE syntax] uzyskać więcej informacji dotyczących tworzenia tabel w magazynie danych SQL.

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
