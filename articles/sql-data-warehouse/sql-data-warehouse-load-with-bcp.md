---
title: "aaaUse bcp tooload danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, czym jest program bcp i jak toouse go w scenariuszach dotyczących magazynów danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>Ładowanie danych za pomocą narzędzia BCP
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[Narzędzie BCP] [ bcp]**  to narzędzie obciążenia zbiorczego wiersza polecenia, które pozwala toocopy danych między programami SQL Server, plików danych i magazyn danych SQL. Za pomocą narzędzia bcp tooimport dużą liczbę wierszy do tabel SQL Data Warehouse lub tooexport dane z tabel programu SQL Server do plików danych. Z wyjątkiem przypadków obejmujących użycie opcji queryout hello bcp nie wymaga żadnej znajomości języka Transact-SQL.

BCP można szybko i łatwo toomove mniejszych zestawów danych do i z bazy danych SQL Data Warehouse. zależy od rodzaju Hello dokładną ilość danych zaleca się tooload/wyodrębniania za pomocą narzędzia bcp w sieci centrum danych Azure toohello połączenia.  Ogólnie rzecz biorąc, przy użyciu narzędzia bcp można łatwo ładować tabele wymiarów i wyodrębniać z nich dane, jednak narzędzie to nie jest zalecane dla ładowania lub wyodrębniania dużych ilości danych.  Program Polybase jest hello zalecane narzędziem do ładowania i wyodrębnianie dużych ilości danych, jak lepiej zadanie, wykorzystując architekturę masowego przetwarzania równoległego hello usługi SQL Data Warehouse.

Narzędzie bcp umożliwia:

* Użyj danych tooload prostego narzędzia wiersza polecenia do usługi SQL Data Warehouse.
* Użyj danych tooextract prostego narzędzia wiersza polecenia z magazynu danych SQL.

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Importowanie danych do tabeli za pomocą narzędzia bcp hello w poleceniu
* Eksportowanie danych z tabeli budynkach hello polecenia bcp out

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
toostep opisanych w tym samouczku, potrzebne są:

* Baza danych usługi SQL Data Warehouse
* zainstalowane narzędzie wiersza polecenia bcp Hello
* Witaj zainstalowane narzędzie wiersza polecenia SQLCMD

> [!NOTE]
> Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importowanie danych do usługi SQL Data Warehouse
W tym samouczku utworzysz tabelę w usłudze Azure SQL Data Warehouse i zaimportuj dane do tabeli hello.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Krok 1: tworzenie tabeli w usłudze Azure SQL Data Warehouse
Z wiersza polecenia użyj następującego zapytania toocreate tabeli w wystąpieniu hello toorun sqlcmd:

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

> [!NOTE]
> Zobacz [omówienie tabeli] [ Table Overview] lub [składni polecenia CREATE TABLE] [ CREATE TABLE syntax] Aby uzyskać więcej informacji dotyczących tworzenia tabel SQL Data Warehouse i hello  Opcje dostępne w klauzuli WITH hello.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Krok 2: tworzenie źródłowego pliku danych
Otwórz hello Notatnik i skopiuj następujące wiersze danych do nowego pliku tekstowego, a następnie zapisz ten plik tooyour lokalnym katalogu tymczasowym, C:\Temp\DimDate2.txt.

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

> [!NOTE]
> Jest ważne tooremember program bcp.exe nie obsługuje kodowania pliku hello UTF-8. Podczas korzystania z programu bcp.exe należy używać plików kodowanych w formacie ASCII lub UTF-16.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Krok 3: Łączenie i zaimportuj dane hello
Przy użyciu narzędzia bcp, możesz łączyć i zaimportować dane hello przy użyciu hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Można sprawdzić hello załadowania danych, uruchamiając następujące zapytanie przy użyciu narzędzia sqlcmd hello:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Powinny zostać zwrócone hello następujące wyniki:

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Krok 4: tworzenie statystyk na podstawie nowo załadowanych danych
Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk. W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello. Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów. Poniżej przedstawiono sposób toocreate statystyk na powitania przedłożenia załadowany w tym przykładzie przedstawiono prosty przykład

Wykonaj następujące instrukcję CREATE STATISTICS w wierszu polecenia sqlcmd hello:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Eksportowanie danych z usługi SQL Data Warehouse
W tym samouczku utworzysz plik danych z tabeli w usłudze SQL Data Warehouse. Firma Microsoft będzie eksportować hello wyeksportujemy dane utworzone powyżej tooa nowy plik danych o nazwie DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Krok 1: Eksportowanie danych hello
Przy użyciu narzędzia bcp hello, możesz łączyć i wyeksportować dane za pomocą hello następujące polecenia zastąpienie wartości hello zależnie od potrzeb:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Możesz sprawdzić powitalne dane zostały poprawnie wyeksportowane, otwierając nowy plik hello. Witaj dane w pliku hello powinny odpowiadać tekstowi hello poniżej:

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

> [!NOTE]
> Powodu toohello specyfikę systemów rozproszonych kolejność danych hello nie może być takie same hello między bazami danych magazynu danych SQL. Innym rozwiązaniem jest toouse hello **queryout** funkcja toowrite bcp zapytanie wyodrębniające, zamiast eksportować całą tabelę hello.
> 
> 

## <a name="next-steps"></a>Następne kroki
Omówienie ładowania można znaleźć w artykule [Ładowanie danych do usługi SQL Data Warehouse][Load data into SQL Data Warehouse].
Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].

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
