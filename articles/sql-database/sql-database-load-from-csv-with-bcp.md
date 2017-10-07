---
title: plik danych aaaLoad z pliku CSV do bazy danych SQL Azure (bcp) | Dokumentacja firmy Microsoft
description: "Rozmiar danych w małych używa bcp tooimport danych do bazy danych SQL Azure."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>Ładowanie danych z pliku CSV do usługi Azure SQL Database (pliki proste)
W bazie danych SQL Azure, można użyć danych tooimport narzędzia wiersza polecenia bcp hello z pliku CSV.

## <a name="before-you-begin"></a>Przed rozpoczęciem
### <a name="prerequisites"></a>Wymagania wstępne
Witaj toocomplete kroków w tym artykule, należy:

* Serwer logiczny i baza danych usługi Azure SQL Database
* Narzędzie wiersza polecenia bcp Hello zainstalowany
* narzędzia wiersza polecenia sqlcmd Hello zainstalowany

Witaj narzędzia bcp i sqlcmd można pobrać z hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Dane w formacie ASCII lub UTF-16
W przypadku tego samouczka z użyciem własnych danych, dane wymagają toouse hello ASCII lub kodowania UTF-16, ponieważ narzędzie bcp nie obsługuje UTF-8. 

## <a name="1-create-a-destination-table"></a>1. Tworzenie tabeli docelowej
Zdefiniuj tabelę w bazie danych SQL jako hello tabeli docelowej. Witaj kolumn w tabeli hello musi odpowiadać toohello danych w poszczególnych wierszach pliku danych.

toocreate tabelę, otwórz wiersz polecenia i użyj hello toorun sqlcmd.exe następujące polecenie:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Ładowanie danych hello
tooload hello danych, otwórz wiersz polecenia i uruchom hello następujące polecenie, zastępując hello wartości dla nazwy serwera, nazwę bazy danych, nazwę użytkownika i hasło z odpowiednimi informacjami.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Użyj tego polecenia tooverify hello dane zostały załadowane poprawnie

```bcp
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

## <a name="next-steps"></a>Następne kroki
toomigrate bazy danych programu SQL Server, zobacz [migracja bazy danych programu SQL Server](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
