## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Określanie struktury definicji dla prostokątnego zestawów danych
Witaj struktury sekcja w zestawach danych hello JSON jest **opcjonalne** sekcji prostokątne tabel (wiersze i kolumny) i zawiera zestaw kolumn dla tabeli hello. Użyjesz hello struktura sekcji albo udostępnienie informacji o typie dla konwersje typów lub wykonując mapowania kolumn. Hello w następujących sekcjach opisano te funkcje szczegółowo. 

Każda kolumna zawiera hello następujące właściwości:

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| name |Nazwa kolumny hello. |Tak |
| type |Typ danych kolumny hello. Zobacz szczegółowe typu konwersje poniższej sekcji dotyczące kiedy należy określić informacje o typie |Nie |
| Kultury |.NET na podstawie toobe kultura używana, gdy typ jest określona i jest typ architektury .NET, Datetime i Datetimeoffset. Domyślna to "en-us". |Nie |
| Format |Format ciągu toobe używany, gdy typ jest określona i jest typ architektury .NET, Datetime i Datetimeoffset. |Nie |

Witaj poniższy przykład przedstawia hello struktura sekcji JSON dla tabeli, która ma trzy kolumny userid, nazwy i lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Użyj następujących wytycznych program hello tooinclude "structure" informacji i jakie tooinclude w hello **struktury** sekcji.

* **Dla źródeł danych strukturalnych** który przechowują informacje schematu i typu danych wraz z samych (źródeł, takich jak SQL Server, Oracle, tabeli platformy Azure itp.), należy określić sekcji "struktury" hello, tylko jeśli mapowania kolumn określonych danych hello kolumny źródłowej, które kolumny toospecific w ich nazwy i ujście są hello nie sam (Zobacz szczegóły w poniższej sekcji mapowanie kolumn). 
  
    Jak wspomniano powyżej, informacje o typie hello jest opcjonalna w sekcji "structure". Strukturalne źródeł informacji o typie jest już dostępna jako część definicji zestawu danych w magazynie danych hello, więc nie należy używać informacji o typie zawierają hello sekcji "structure".
* **Do schematu w źródłach danych odczytu (w szczególności obiektów blob platformy Azure)** toostore danych można wybrać bez żadnych informacji schematu i typu danych hello przechowywania. W przypadku tych typów źródeł danych, należy uwzględnić "structure" w powitania po 2 przypadkach:
  * Ma toodo mapowania kolumn.
  * Zestaw danych hello jest źródłem w działaniu kopiowania, możesz podać informacje o typie w "structure", a fabryki danych użyje tych informacji typu dla konwersji typów toonative dla obiekt sink hello. Zobacz [Przenieś tooand danych z obiektu Blob Azure](../articles/data-factory/data-factory-azure-blob-connector.md) artykułu, aby uzyskać więcej informacji.

### <a name="supported-net-based-types"></a>Obsługiwane. Typy sieci
Witaj obsługuje fabryki danych po .NET zgodne ze specyfikacją CLS na podstawie wartości typu udostępnienie informacji o typie w "structure" dla schematu na źródeł danych odczytu, takich jak obiektów blob platformy Azure.

* Int16
* Int32 
* Int64
* Pojedynczy
* O podwójnej precyzji
* Decimal
* Byte]
* wartość logiczna
* Ciąg 
* Identyfikator GUID
* Data i godzina
* Datetimeoffset
* Zakres czasu 

Dla typu Datetime i Datetimeoffset również opcjonalnie można określić "Kultura" & "format" ciągu toofacilitate analizowania niestandardowego ciągu daty/godziny. Zobacz przykład poniżej konwersji typu.

