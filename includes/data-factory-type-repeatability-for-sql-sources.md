## <a name="repeatability-during-copy"></a><span data-ttu-id="f5809-101">Powtarzalność podczas kopiowania</span><span class="sxs-lookup"><span data-stu-id="f5809-101">Repeatability during Copy</span></span>
<span data-ttu-id="f5809-102">Podczas kopiowania danych tooAzure SQL/programu SQL Server z innymi danymi przechowuje jeden powtarzalności tookeep potrzeb w tooavoid zdanie niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="f5809-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="f5809-103">Podczas kopiowania danych tooAzure bazy danych serwera SQL/SQL, działanie kopiowania zostanie przez domyślny APPEND hello zestawu danych toohello zbiornika tabelę domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f5809-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="f5809-104">Na przykład podczas kopiowania danych z źródła pliku CSV (dane wartości rozdzielonych przecinkami) zawierającego dwa rekordy tooAzure bazy danych SQL/SQL Server, to jakie tabeli hello wygląda jak:</span><span class="sxs-lookup"><span data-stu-id="f5809-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="f5809-105">Załóżmy, że znaleziono błędy w pliku źródłowym i ilość zaktualizowane hello przewodu w dół od 2 too4 w pliku źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="f5809-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="f5809-106">Wycinek danych hello uruchomić ponownie dla tego okresu, przekonasz się, że dwa nowe rekordy dołączany tooAzure bazy danych serwera SQL/SQL.</span><span class="sxs-lookup"><span data-stu-id="f5809-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="f5809-107">Witaj poniżej założono, że żadna hello kolumn w tabeli hello nie ma ograniczenia klucza podstawowego hello.</span><span class="sxs-lookup"><span data-stu-id="f5809-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="f5809-108">tooavoid, konieczne będzie semantyki UPSERT toospecify przez wykorzystanie jednej z hello poniżej 2 mechanizmów podaną poniżej.</span><span class="sxs-lookup"><span data-stu-id="f5809-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="f5809-109">Wycinek można uruchomić ponownie automatycznie w fabryce danych Azure zgodnie z harmonogramem hello zasady ponawiania określone.</span><span class="sxs-lookup"><span data-stu-id="f5809-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="f5809-110">Mechanizm 1</span><span class="sxs-lookup"><span data-stu-id="f5809-110">Mechanism 1</span></span>
<span data-ttu-id="f5809-111">Można wykorzystać **sqlWriterCleanupScript** toofirst właściwości wykonania akcji oczyszczania po uruchomieniu wycinek.</span><span class="sxs-lookup"><span data-stu-id="f5809-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="f5809-112">Witaj skrypt czyszczący będzie można wykonać pierwsze podczas kopiowania dla danego wycinka, co spowoduje usunięcie danych hello z odpowiedniego wycinka toothat hello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="f5809-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="f5809-113">działanie Hello zostanie następnie wstawianie danych hello w hello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="f5809-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="f5809-114">Jeśli wycinek hello jest teraz ponownie uruchomić, a następnie można tam znaleźć ilość hello jest aktualizowana jako wymaganą.</span><span class="sxs-lookup"><span data-stu-id="f5809-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="f5809-115">Załóżmy, że hello podkładka prosty rekord zostanie usunięte z oryginalnej csv hello.</span><span class="sxs-lookup"><span data-stu-id="f5809-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="f5809-116">Następnie ponowne uruchomienie wycinek hello dałby w efekcie hello następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="f5809-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="f5809-117">Żadne nowe miał toobe gotowe.</span><span class="sxs-lookup"><span data-stu-id="f5809-117">Nothing new had toobe done.</span></span> <span data-ttu-id="f5809-118">działanie kopiowania Hello uruchomiono hello oczyszczania toodelete hello odpowiednich danych skryptu dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="f5809-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="f5809-119">Następnie on hello danych wejściowych do odczytu z pliku csv hello, (który następnie zawiera tylko 1 rekord) i dodaje go do hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="f5809-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="f5809-120">Mechanizm 2</span><span class="sxs-lookup"><span data-stu-id="f5809-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5809-121">w tej chwili sliceIdentifierColumnName nie jest obsługiwana dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f5809-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="f5809-122">Inny mechanizm tooachieve powtarzalności jest wprowadzenie dedykowanego kolumny (**sliceIdentifierColumnName**) w hello target tabeli.</span><span class="sxs-lookup"><span data-stu-id="f5809-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="f5809-123">W tej kolumnie mogą być wykorzystane przez fabryki danych Azure tooensure hello źródłowego i docelowego Pozostań zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="f5809-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="f5809-124">Ta metoda działa po elastyczność zmiana lub definiowania schematu SQL tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="f5809-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="f5809-125">Ta kolumna będzie używany przez fabryki danych Azure na potrzeby celów powtarzalność i w procesie hello fabryki danych Azure nie dokona żadnych schematu zmiany toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="f5809-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="f5809-126">Sposób toouse tego podejścia:</span><span class="sxs-lookup"><span data-stu-id="f5809-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="f5809-127">Zdefiniuj kolumna typu binary (32) w lokalizacji docelowej hello tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="f5809-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="f5809-128">Nie powinno być nie ograniczeń dla tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="f5809-128">There should be no constraints on this column.</span></span> <span data-ttu-id="f5809-129">Teraz nazwę tej kolumny jako "ColumnForADFuseOnly" w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f5809-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="f5809-130">Należy użyć go w przypadku działania kopiowania hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f5809-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="f5809-131">Fabryka danych Azure zostaną wyświetlone w tej kolumnie zgodnie z jego potrzeby tooensure hello źródłowym i docelowym zachować synchronizację.</span><span class="sxs-lookup"><span data-stu-id="f5809-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="f5809-132">Witaj wartości tej kolumny nie powinna być używana poza tym kontekście przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="f5809-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="f5809-133">Podobne toomechanism 1, działanie kopiowania zostanie automatycznie pierwszy czyszczenie danych hello na powitania, biorąc pod uwagę wycinek z hello docelowej tabeli SQL, a następnie uruchom działanie kopiowania hello zwykle tooinsert hello danych z toodestination źródła dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="f5809-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

