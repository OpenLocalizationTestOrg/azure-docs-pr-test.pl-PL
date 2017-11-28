## <a name="repeatability-during-copy"></a><span data-ttu-id="29d7d-101">Powtarzalność podczas kopiowania</span><span class="sxs-lookup"><span data-stu-id="29d7d-101">Repeatability during Copy</span></span>
<span data-ttu-id="29d7d-102">Jeśli kopiowanie danych do usługi Azure SQL/programu SQL Server z innymi danymi przechowuje należy należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="29d7d-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="29d7d-103">Podczas kopiowania danych do bazy danych serwera SQL/SQL Azure, działanie kopiowania zostanie domyślnie Dołącz zestaw danych do tabeli ujścia domyślnie.</span><span class="sxs-lookup"><span data-stu-id="29d7d-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="29d7d-104">Na przykład podczas kopiowania danych z źródła pliku CSV (dane wartości rozdzielonych przecinkami) zawierającego dwa rekordy do bazy danych serwera SQL/SQL Azure, jest tabela wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="29d7d-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="29d7d-105">Załóżmy, że znaleziono błędy w pliku źródłowym i zaktualizować ilość przewodu w dół od 2 do 4 w pliku źródłowym.</span><span class="sxs-lookup"><span data-stu-id="29d7d-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="29d7d-106">Jeśli uruchomisz ponownie wycinek danych dla tego okresu, znajdują się dwie nowe rekordy dołączane do bazy danych serwera SQL/SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="29d7d-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="29d7d-107">Poniżej założono, żaden z kolumn w tabeli nie ma ograniczenia klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="29d7d-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="29d7d-108">Aby tego uniknąć, należy określić semantykę UPSERT przez wykorzystanie jednej z poniższych 2 mechanizmów podaną poniżej.</span><span class="sxs-lookup"><span data-stu-id="29d7d-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="29d7d-109">Wycinek może zostać ponownie uruchomione automatycznie w fabryce danych Azure zgodnie z harmonogramem zasady ponawiania określone.</span><span class="sxs-lookup"><span data-stu-id="29d7d-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="29d7d-110">Mechanizm 1</span><span class="sxs-lookup"><span data-stu-id="29d7d-110">Mechanism 1</span></span>
<span data-ttu-id="29d7d-111">Można wykorzystać **sqlWriterCleanupScript** właściwości, aby najpierw wykonać akcję czyszczenia po uruchomieniu wycinek.</span><span class="sxs-lookup"><span data-stu-id="29d7d-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="29d7d-112">Skrypt czyszczący będzie można wykonać pierwsze podczas kopiowania dla danego wycinka, co spowoduje usunięcie danych z tabeli SQL odpowiadający tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="29d7d-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="29d7d-113">Działanie zostanie następnie wstawianie danych do tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="29d7d-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="29d7d-114">Jeśli wycinek jest teraz ponownie uruchomić, a następnie można tam znaleźć ilość jest aktualizowana jako wymaganą.</span><span class="sxs-lookup"><span data-stu-id="29d7d-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="29d7d-115">Załóżmy, że rekord płaskiej podkładka zostanie usunięte z oryginalnej csv.</span><span class="sxs-lookup"><span data-stu-id="29d7d-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="29d7d-116">Ponowne uruchomienie wycinka dałby w efekcie następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="29d7d-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="29d7d-117">Żadne nowe musiało być przeprowadzane.</span><span class="sxs-lookup"><span data-stu-id="29d7d-117">Nothing new had to be done.</span></span> <span data-ttu-id="29d7d-118">Działanie kopiowania uruchomiono skrypt czyszczący do usuwania odpowiednich danych dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="29d7d-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="29d7d-119">A następnie go odczytać dane wejściowe z plików csv (który następnie zawiera tylko 1 rekord) i dodaje go do tabeli.</span><span class="sxs-lookup"><span data-stu-id="29d7d-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="29d7d-120">Mechanizm 2</span><span class="sxs-lookup"><span data-stu-id="29d7d-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="29d7d-121">w tej chwili sliceIdentifierColumnName nie jest obsługiwana dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="29d7d-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="29d7d-122">Innym mechanizmem do osiągnięcia powtarzalności jest wprowadzenie dedykowanego kolumny (**sliceIdentifierColumnName**) w tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="29d7d-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="29d7d-123">W tej kolumnie będzie służyć przez fabryki danych Azure, aby upewnić się, że na serwerze źródłowym i docelowym zachować synchronizację.</span><span class="sxs-lookup"><span data-stu-id="29d7d-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="29d7d-124">Ta metoda działa po elastyczność zmiana lub definiowania schematu SQL tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="29d7d-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="29d7d-125">Ta kolumna będzie używany przez fabryki danych Azure na potrzeby celów powtarzalność i w procesie fabryki danych Azure nie dokona żadnych zmian schematu do tabeli.</span><span class="sxs-lookup"><span data-stu-id="29d7d-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="29d7d-126">Sposób użycia tej metody:</span><span class="sxs-lookup"><span data-stu-id="29d7d-126">Way to use this approach:</span></span>

1. <span data-ttu-id="29d7d-127">W docelowej tabeli SQL, należy zdefiniować kolumnę z danymi typu binarnego (32).</span><span class="sxs-lookup"><span data-stu-id="29d7d-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="29d7d-128">Nie powinno być nie ograniczeń dla tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="29d7d-128">There should be no constraints on this column.</span></span> <span data-ttu-id="29d7d-129">Teraz nazwę tej kolumny jako "ColumnForADFuseOnly" w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="29d7d-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="29d7d-130">Należy użyć go w przypadku działania kopiowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="29d7d-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="29d7d-131">Fabryka danych Azure są powielane tej kolumny, trzeba upewnić się, że na serwerze źródłowym i docelowym zachować synchronizację zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="29d7d-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="29d7d-132">Wartości tej kolumny powinien nie używane poza tym kontekście przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="29d7d-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="29d7d-133">Podobnie do mechanizmu 1, działanie kopiowania zostanie automatycznie najpierw wyczyścić dane dla wycinka danego przeznaczenia tabeli SQL, a następnie uruchomić działanie kopiowania normalnie, aby wstawić dane ze źródła do miejsca docelowego dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="29d7d-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

