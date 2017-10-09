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
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="e9f4a-103">Kopiuj powtarzalne w fabryce danych Azure</span><span class="sxs-lookup"><span data-stu-id="e9f4a-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e9f4a-104">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="e9f4a-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="e9f4a-105">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e9f4a-106">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e9f4a-107">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e9f4a-108">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="e9f4a-109">Witaj następujące przykłady są dla bazy danych SQL Azure, ale są odpowiednie tooany magazynem danych, który obsługuje prostokątne zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="e9f4a-110">Masz tooadjust hello **typu** źródła i hello **zapytania** właściwości (na przykład: zapytanie, zamiast sqlReaderQuery) danych hello przechowywania.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="e9f4a-111">Zazwyczaj podczas odczytu z relacyjnych magazynów, ma tooread wyłącznie dane hello odpowiadającego toothat wycinka.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="e9f4a-112">Toodo sposób będzie więc przy użyciu hello WindowStart i WindowEnd zmienne systemowe dostępne w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="e9f4a-113">Przeczytaj informacje o zmiennych hello i funkcji w fabryce danych Azure w hello [fabryki danych Azure — funkcje i zmienne systemu](data-factory-functions-variables.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="e9f4a-114">Przykład:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="e9f4a-115">To zapytanie odczytuje dane, która znajduje się w zakresie czasu trwania wycinek hello (WindowStart -> WindowEnd) z tabeli hello MyTable.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="e9f4a-116">Uruchom ponownie tego wycinka będzie zawsze upewnij się, że hello odczytywania tych samych danych.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="e9f4a-117">W innych przypadkach może być wymagane tooread hello całej tabeli i może zdefiniować hello sqlReaderQuery w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="e9f4a-118">TooSqlSink powtarzalne zapisu</span><span class="sxs-lookup"><span data-stu-id="e9f4a-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="e9f4a-119">Podczas kopiowania danych zbyt**Azure SQL/programu SQL Server** od innych magazynów danych należy tookeep powtarzalności tooavoid uwadze niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="e9f4a-120">Podczas kopiowania danych tooAzure bazy danych serwera SQL/SQL, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="e9f4a-121">Przykład kopiujesz danych CSV (wartości rozdzielane przecinkami) pliku zawierającego dwa rekordy toohello w poniższej tabeli w bazie danych Azure SQL/programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="e9f4a-122">Po uruchomieniu wycinek hello dwa rekordy są kopiowane toohello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="e9f4a-123">Załóżmy, że znaleziono błędy w pliku źródłowym i zaktualizować ilość hello przewodu w dół od 2 too4.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="e9f4a-124">Jeśli uruchomisz hello wycinek danych dla tego okresu ręcznie, znajdują się, że dwa nowe rekordy dołączany tooAzure bazy danych SQL/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="e9f4a-125">W tym przykładzie założono, że żaden z hello kolumn w tabeli hello nie ma hello ograniczenia klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="e9f4a-126">tooavoid to zachowanie, należy semantyki UPSERT toospecify przy użyciu jednej z hello następujące dwa mechanizmy:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="e9f4a-127">Mechanizmu 1: sqlWriterCleanupScript przy użyciu</span><span class="sxs-lookup"><span data-stu-id="e9f4a-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="e9f4a-128">Można użyć hello **sqlWriterCleanupScript** tooclean właściwości zapasową danych z tabeli ujścia hello przed wstawieniem danych powitania po uruchomieniu wycinek.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="e9f4a-129">Po uruchomieniu wycinek hello oczyszczania skrypt jest uruchamiany pierwszy danych toodelete odpowiadający toohello wycinek z tabeli SQL hello.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="e9f4a-130">działanie kopiowania Hello Wstawianie danych do hello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="e9f4a-131">Jeśli ponownego uruchomienia wycinka hello ilość hello jest aktualizowana pożądane.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="e9f4a-132">Załóżmy, że hello podkładka prosty rekord zostanie usunięte z oryginalnej csv hello.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="e9f4a-133">Następnie ponowne uruchomienie wycinek hello dałby w efekcie hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="e9f4a-134">działanie kopiowania Hello uruchomiono hello oczyszczania toodelete hello odpowiednich danych skryptu dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="e9f4a-135">Następnie on hello danych wejściowych do odczytu z pliku csv hello, (który następnie zawiera tylko jeden rekord) i dodaje go do hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="e9f4a-136">Mechanizmu 2: sliceIdentifierColumnName przy użyciu</span><span class="sxs-lookup"><span data-stu-id="e9f4a-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9f4a-137">Obecnie sliceIdentifierColumnName nie jest obsługiwana dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="e9f4a-138">Powtarzalność tooachieve mechanizmu drugi Hello jest wprowadzenie dedykowanych kolumny (sliceIdentifierColumnName) w celu hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="e9f4a-139">W tej kolumnie mogą być wykorzystane przez fabryki danych Azure tooensure hello źródłowego i docelowego Pozostań zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="e9f4a-140">Ta metoda działa po elastyczność zmiana lub definiowania schematu SQL tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="e9f4a-141">W tej kolumnie jest używany przez fabryki danych Azure do celów powtarzalność i w procesie hello fabryki danych Azure nie powoduje żadnych schematu zmiany toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="e9f4a-142">Sposób toouse tego podejścia:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="e9f4a-143">Zdefiniuj kolumny typu **danych binarnych (32)** w lokalizacji docelowej hello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="e9f4a-144">Nie powinno być nie ograniczeń dla tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-144">There should be no constraints on this column.</span></span> <span data-ttu-id="e9f4a-145">Teraz nazwę tej kolumny jako AdfSliceIdentifier w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="e9f4a-146">Tabela źródłowa:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="e9f4a-147">Tabela docelowa:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="e9f4a-148">Należy użyć go w przypadku działania kopiowania hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="e9f4a-149">Fabryka danych Azure wypełnia tej kolumny, zgodnie z jego potrzeby tooensure hello źródłowym i docelowym zachować synchronizację.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="e9f4a-150">poza tym kontekście nie można używać Hello wartości tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="e9f4a-151">Podobne toomechanism 1, działanie kopiowania automatycznie oczyszcza dane hello hello, biorąc pod uwagę wycinek z hello docelowej tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="e9f4a-152">Następnie wstawia dane ze źródła w tabeli docelowej toohello.</span><span class="sxs-lookup"><span data-stu-id="e9f4a-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e9f4a-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9f4a-153">Next steps</span></span>
<span data-ttu-id="e9f4a-154">Przejrzyj następujące artykuły łącznika, które dla ukończyć przykłady JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e9f4a-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="e9f4a-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e9f4a-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="e9f4a-156">Magazyn danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e9f4a-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="e9f4a-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e9f4a-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)