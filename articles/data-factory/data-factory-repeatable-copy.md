---
title: Kopiuj aaaRepeatable w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooavoid duplikatów, nawet jeśli wycinek, który kopiuje dane jest uruchamiana w więcej niż raz."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Kopiuj powtarzalne w fabryce danych Azure

## <a name="repeatable-read-from-relational-sources"></a>Odczyt powtarzalny ze źródłami relacyjnymi
Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników. Fabryka danych Azure możesz ponownie ręcznie wycinek. Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd. W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.  
 
> [!NOTE]
> Witaj następujące przykłady są dla bazy danych SQL Azure, ale są odpowiednie tooany magazynem danych, który obsługuje prostokątne zestawów danych. Masz tooadjust hello **typu** źródła i hello **zapytania** właściwości (na przykład: zapytanie, zamiast sqlReaderQuery) danych hello przechowywania.   

Zazwyczaj podczas odczytu z relacyjnych magazynów, ma tooread wyłącznie dane hello odpowiadającego toothat wycinka. Toodo sposób będzie więc przy użyciu hello WindowStart i WindowEnd zmienne systemowe dostępne w fabryce danych Azure. Przeczytaj informacje o zmiennych hello i funkcji w fabryce danych Azure w hello [fabryki danych Azure — funkcje i zmienne systemu](data-factory-functions-variables.md) artykułu. Przykład: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
To zapytanie odczytuje dane, która znajduje się w zakresie czasu trwania wycinek hello (WindowStart -> WindowEnd) z tabeli hello MyTable. Uruchom ponownie tego wycinka będzie zawsze upewnij się, że hello odczytywania tych samych danych. 

W innych przypadkach może być wymagane tooread hello całej tabeli i może zdefiniować hello sqlReaderQuery w następujący sposób:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>TooSqlSink powtarzalne zapisu
Podczas kopiowania danych zbyt**Azure SQL/programu SQL Server** od innych magazynów danych należy tookeep powtarzalności tooavoid uwadze niezamierzone wyników. 

Podczas kopiowania danych tooAzure bazy danych serwera SQL/SQL, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie. Przykład kopiujesz danych CSV (wartości rozdzielane przecinkami) pliku zawierającego dwa rekordy toohello w poniższej tabeli w bazie danych Azure SQL/programu SQL Server. Po uruchomieniu wycinek hello dwa rekordy są kopiowane toohello tabeli SQL. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Załóżmy, że znaleziono błędy w pliku źródłowym i zaktualizować ilość hello przewodu w dół od 2 too4. Jeśli uruchomisz hello wycinek danych dla tego okresu ręcznie, znajdują się, że dwa nowe rekordy dołączany tooAzure bazy danych SQL/SQL Server. W tym przykładzie założono, że żaden z hello kolumn w tabeli hello nie ma hello ograniczenia klucza podstawowego.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid to zachowanie, należy semantyki UPSERT toospecify przy użyciu jednej z hello następujące dwa mechanizmy:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mechanizmu 1: sqlWriterCleanupScript przy użyciu
Można użyć hello **sqlWriterCleanupScript** tooclean właściwości zapasową danych z tabeli ujścia hello przed wstawieniem danych powitania po uruchomieniu wycinek. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Po uruchomieniu wycinek hello oczyszczania skrypt jest uruchamiany pierwszy danych toodelete odpowiadający toohello wycinek z tabeli SQL hello. działanie kopiowania Hello Wstawianie danych do hello tabeli SQL. Jeśli ponownego uruchomienia wycinka hello ilość hello jest aktualizowana pożądane.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Załóżmy, że hello podkładka prosty rekord zostanie usunięte z oryginalnej csv hello. Następnie ponowne uruchomienie wycinek hello dałby w efekcie hello następujące wyniki: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

działanie kopiowania Hello uruchomiono hello oczyszczania toodelete hello odpowiednich danych skryptu dla tego wycinka. Następnie on hello danych wejściowych do odczytu z pliku csv hello, (który następnie zawiera tylko jeden rekord) i dodaje go do hello tabeli. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mechanizmu 2: sliceIdentifierColumnName przy użyciu
> [!IMPORTANT]
> Obecnie sliceIdentifierColumnName nie jest obsługiwana dla usługi Azure SQL Data Warehouse. 

Powtarzalność tooachieve mechanizmu drugi Hello jest wprowadzenie dedykowanych kolumny (sliceIdentifierColumnName) w celu hello tabeli. W tej kolumnie mogą być wykorzystane przez fabryki danych Azure tooensure hello źródłowego i docelowego Pozostań zsynchronizowane. Ta metoda działa po elastyczność zmiana lub definiowania schematu SQL tabeli docelowej hello. 

W tej kolumnie jest używany przez fabryki danych Azure do celów powtarzalność i w procesie hello fabryki danych Azure nie powoduje żadnych schematu zmiany toohello tabeli. Sposób toouse tego podejścia:

1. Zdefiniuj kolumny typu **danych binarnych (32)** w lokalizacji docelowej hello tabeli SQL. Nie powinno być nie ograniczeń dla tej kolumny. Teraz nazwę tej kolumny jako AdfSliceIdentifier w tym przykładzie.


    Tabela źródłowa:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Tabela docelowa: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Należy użyć go w przypadku działania kopiowania hello w następujący sposób:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Fabryka danych Azure wypełnia tej kolumny, zgodnie z jego potrzeby tooensure hello źródłowym i docelowym zachować synchronizację. poza tym kontekście nie można używać Hello wartości tej kolumny. 

Podobne toomechanism 1, działanie kopiowania automatycznie oczyszcza dane hello hello, biorąc pod uwagę wycinek z hello docelowej tabeli SQL. Następnie wstawia dane ze źródła w tabeli docelowej toohello. 

## <a name="next-steps"></a>Następne kroki
Przejrzyj następujące artykuły łącznika, które dla ukończyć przykłady JSON hello: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)