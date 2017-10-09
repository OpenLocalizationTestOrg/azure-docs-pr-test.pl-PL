---
title: aaa "interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB: składnia SQL | Opis elementu Microsoft Docs": odwołanie dokumentacji hello język zapytań SQL interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB.
usługi: Autor db rozwiązania cosmos: Menedżera mimig1: Edytor jhubbard: mimig documentationcenter: "

MS.AssetID: ms.service: ms.workload db rozwiązania cosmos: ms.tgt_pltfrm usług danych: na ms.devlang: na ms.topic: odwołanie ms.date: ms.author 2017-06/13: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>Azure DocumentDB rozwiązania Cosmos DB interfejsu API: Odwołania do składni SQL

Hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB obsługuje tworzenie zapytań dla dokumentów za pomocą znanych SQL (Structured Query Language) jak gramatyki przez hierarchiczna dokumentów JSON bez konieczności jawnego schematu lub tworzenia indeksów pomocniczych. Ten temat zawiera dokumentację referencyjną dla hello język zapytań SQL usługi DocumentDB interfejsu API.

Aby uzyskać wskazówki hello język zapytań SQL usługi DocumentDB interfejsu API, zobacz [kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB](documentdb-sql-query.md).  
  
Również zachęcamy toovisit hello [Plac zabaw dla zapytań](http://www.documentdb.com/sql/demo) gdzie spróbuj bazy danych rozwiązania Cosmos Azure i wykonywania kwerend SQL do naszego zestawu danych.  
  
## <a name="select-query"></a>Zapytanie SELECT  
Pobiera dokumentów JSON z hello bazy danych. Obsługuje oceny wyrażenia, projekcji, filtrowania i tworzy sprzężenie.  konwencje Hello opisujących hello instrukcji "SELECT" wyszczególniono w hello sekcji konwencje składni.  
  
**Składnia**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Uwagi**  
  
 Zobacz następujące sekcje, aby uzyskać szczegółowe informacje na każdej klauzuli:  
  
-   [Klauzula SELECT](#bk_select_query)  
  
-   [Klauzula FROM](#bk_from_clause)  
  
-   [Klauzula WHERE](#bk_where_clause)  
  
-   [Klauzula ORDER BY](#bk_orderby_clause)  
  
klauzule Hello w instrukcji SELECT hello muszą być uporządkowane, jak pokazano powyżej. Jeden z hello opcjonalna klauzula można pominąć. Jednak w przypadku używania klauzule opcjonalne muszą występować w odpowiedniej kolejności hello.  
  
**Logiczna kolejność przetwarzania hello instrukcji SELECT**  
  
Witaj kolejność przetwarzania klauzule jest:  

1.  [Klauzula FROM](#bk_from_clause)  
2.  [Klauzula WHERE](#bk_where_clause)  
3.  [Klauzula ORDER BY](#bk_orderby_clause)  
4.  [Klauzula SELECT](#bk_select_query)  

Należy pamiętać, że jest inna niż kolejność hello, w jakiej występują w składni hello. porządkowanie Hello jest taka, że wszystkie nowe symbole wynikające z klauzulą przetworzonych są widoczne i mogą być używane w klauzulach później przetwarzane. Na przykład w przypadku gdy aliasów zadeklarować w klauzuli FROM są dostępne i klauzule SELECT.  

**Odstęp i komentarze**  

Wszystkie białe znaki, które nie są częścią ciągu w cudzysłowie lub identyfikator w cudzysłowach nie są częścią gramatyki języka hello i są ignorowane podczas analizy.  

język zapytań Hello obsługuje komentarzy styl T-SQL, takich jak  

-   Instrukcja SQL`-- comment text [newline]`  

Gdy znaków odstępu i komentarze nie ma żadnego znaczenia w gramatyce hello, muszą być używane tooseparate tokenów. Na przykład: `-1e5` jest chwilę jednego tokenu, liczba`: – 1 e5` minus token następuje numer 1 i identyfikatora e5.  

##  <a name="bk_select_query"></a>Klauzula SELECT  
klauzule Hello w instrukcji SELECT hello muszą być uporządkowane, jak pokazano powyżej. Jeden z hello opcjonalna klauzula można pominąć. Jednak w przypadku używania klauzule opcjonalne muszą występować w odpowiedniej kolejności hello.  

**Składnia**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Argumenty**  
  
 `<select_specification>`  
  
 Ustaw właściwości lub wartości toobe wybrane dla wyniku hello.  
  
 `'*'`  
  
Określa, że wartość hello powinny zostać pobrane bez wprowadzania żadnych zmian. W szczególności, jeśli wartość hello przetwarzane jest obiektem, będzie można pobrać wszystkich właściwości.  
  
 `<object_property_list>`  
  
Określa listę hello toobe właściwości pobrać. Wartości zwracane będzie obiekt o właściwości hello określone.  
  
`VALUE`  
  
Określa, że wartość JSON hello powinny zostać pobrane zamiast hello cały obiekt JSON. To, w przeciwieństwie do `<property_list>` nie jest zawijany hello prognozowane wartości w obiekcie.  
  
`<scalar_expression>`  
  
Wyrażenie odpowiadające hello toobe wartość obliczana. Zobacz [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.  
  
**Uwagi**  
  
Witaj `SELECT *` składnia jest prawidłowa, jeśli klauzula FROM została zadeklarowana dokładnie jeden alias. `SELECT *`udostępnia projekcji tożsamości, które mogą być przydatne, jeśli nie projekcji nie jest konieczne. Wybierz * jest prawidłowa, jeśli klauzula FROM określono i wprowadzono tylko jednego źródła danych wejściowych.  
  
Należy pamiętać, że `SELECT <select_list>` i `SELECT *` są "sugar składni" i może być również wyrażona za pomocą prostego instrukcji "SELECT", jak pokazano poniżej.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     odpowiada to:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     odpowiada to:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Zobacz też**  
  
[Wyrażenia skalarne](#bk_scalar_expressions)  
[Klauzula SELECT](#bk_select_query)  
  
##  <a name="bk_from_clause"></a>Klauzula FROM  
Określa źródło hello lub dołączonym do źródła. Klauzula FROM Hello jest opcjonalna. Jeśli nie jest określony, inne klauzule nadal będą wykonywane tak, jakby klauzuli FROM podane pojedynczego dokumentu.  
  
**Składnia**  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
**Argumenty**  
  
`<from_source>`  
  
Określa źródło danych, z lub bez aliasu. Jeśli nie określono aliasu, będzie można wywnioskować na podstawie hello `<collection_expression>` za pomocą następujących reguł:  
  
-   Jeśli wyrażenie hello jest nazwa_kolekcji, nazwa_kolekcji będzie używany jako alias.  
  
-   Jeśli wyrażenie hello jest `<collection_expression>`, property_name, a następnie property_name zostanie użyta jako alias. Jeśli wyrażenie hello jest nazwa_kolekcji, nazwa_kolekcji będzie używany jako alias.  
  
JAKO`input_alias`  
  
Określa, że hello `input_alias` to zbiór wartości zwracanych przez hello bazowy wyrażeniu kolekcji.  
 
`input_alias`W  
  
Określa, że hello `input_alias` powinno reprezentować hello zbiór wartości uzyskane przez Iterowanie po każdej tablica zwrócona przez hello bazowy wyrażeniu kolekcji wszystkie elementy tablicy. Każda wartość zwracana przez podstawowej wyrażeniu kolekcji, która nie jest tablicą jest ignorowana.  
  
`<collection_expression>`  
  
Określa, że hello kolekcji wyrażenie toobe używanych tooretrieve hello dokumentów.  
  
`ROOT`  
  
Określa, że w tym dokumencie powinny zostać pobrane z hello domyślnie kolekcji aktualnie połączonych.  
  
`collection_name`  
  
Określa, że tego dokumentu powinny zostać pobrane z kolekcji hello podane. Nazwa Hello kolekcji hello musi odpowiadać nazwie hello kolekcji hello aktualnie połączony.  
  
`input_alias`  
  
Określa, w tym dokumencie powinny zostać pobrane z hello innego źródła, zdefiniowany przez hello podany alias.  
  
`<collection_expression> '.' property_`  
  
Określa, w tym dokumencie powinny zostać pobrane po zalogowaniu się do hello `property_name` właściwości lub indeks_tablicy elementu tablicy dla wszystkich dokumentów pobierane przez określone wyrażenie kolekcji.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Określa, w tym dokumencie powinny zostać pobrane po zalogowaniu się do hello `property_name` właściwości lub indeks_tablicy elementu tablicy dla wszystkich dokumentów pobierane przez określone wyrażenie kolekcji.  
  
**Uwagi**  
  
Wszystkie aliasy dostarczona lub wywnioskować w hello `<from_source>(`s) musi być unikatowa. Witaj składni `<collection_expression>.`property_name jest identyczny hello `<collection_expression>' ['"property_name"']'`. Jednak hello później można używać składni Jeśli nazwa właściwości zawiera znaki innego niż identyfikator.  
  
**Brak elementów tablicy nie ma właściwości niezdefiniowanych wartości obsługi**  
  
Wyrażeniu kolekcji uzyskuje dostęp do właściwości lub elementów tablicy i że nie ma wartości, tej wartości będą ignorowane i nie można przetworzyć więcej.  
  
**Kolekcja wyrażeń kontekstu zakresu**  
  
Wyrażeniu kolekcji może być zakresem kolekcji lub zakres dokumentu:  
  
-   Wyrażenie jest zakres kolekcji, jeśli hello źródła wyrażeniu kolekcji hello jest albo głównego lub `collection_name`. Takie wyrażenie reprezentuje zestaw dokumentów pobierane z kolekcji hello bezpośrednio i nie jest zależna od przetwarzania hello innych wyrażeń kolekcji.  
  
-   Wyrażenie jest zakres dokumentu, jeśli hello źródła wyrażeniu kolekcji hello jest `input_alias` wprowadzone we wcześniejszej części hello zapytania. Takie wyrażenie reprezentuje zestaw dokumentów uzyskany przez obliczenie hello wyrażeniu kolekcji w zakresie hello każdego dokumentu należących zestaw toohello skojarzony z kolekcją aliasem hello.  Wynikowy zestaw Hello będzie Unii zestawów uzyskany przez obliczenie hello kolekcji wyrażenia dla każdego z dokumentów hello w hello podstawowy zestaw.  
  
**Tworzy sprzężenie**  
  
W bieżącej wersji hello Azure DB rozwiązania Cosmos obsługuje sprzężeń wewnętrznych. Nadchodzącego są sprzężenia dodatkowe funkcje.

Wynik sprzężenia wewnętrzne w pełny iloczyn wektorowy hello ustawia uczestniczących hello sprzężenia. wynik Hello N sposób sprzężenia jest zestaw spójnych kolekcji z elementu N, gdzie każdej wartości w krotce hello jest skojarzony z aliasem hello ustawić uczestniczących hello sprzężenia i jest możliwy za pomocą odwołań do tego aliasu w innych klauzul.  
  
oceny Hello sprzężenia hello zależy od zakresu kontekstu hello hello uczestniczących zestawów:  
  
-  Sprzężenia między kolekcji zestawu A i zakres kolekcji ustawić B, wynikiem iloczyn wektorowy wszystkie elementy w zestawach A i B.
  
-   Powoduje sprzężenie zestaw A i zestaw zakres dokumentu B, w związku z wszystkich zestawów uzyskany przez obliczenie zakres dokumentu zestawu B dla każdego dokumentu z ustawić A.  
  
 W bieżącej wersji hello maksymalnie jedno wyrażenie zakres kolekcji jest obsługiwany przez procesor zapytań hello.  
  
**Przykłady sprzężeń:**  
  
Przyjrzyjmy się powitania po klauzuli FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Let każdego źródła Zdefiniuj `input_alias1, input_alias2, …, input_aliasN`. Tej klauzuli FROM zwraca zestaw spójnych kolekcji na N (krotka z wartościami N). Każda krotka zawiera wartości utworzonego przez Iterowanie wszystkie aliasy kolekcji po ich odpowiednich zestawów.  
  
*Dołącz do SPOŁECZNOŚCI przykład 1 z 2 źródeł:*  
  
- Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.  
  
- Let `<from_source2>` można dokumentu o zakresie odwołujące się do input_alias1 i reprezentują zestawów:  
  
    {1, 2} dla`input_alias1 = A,`  
  
    {3} dla`input_alias1 = B,`  
  
    {4, 5} dla`input_alias1 = C,`  
  
- Witaj w klauzuli FROM `<from_source1> JOIN <from_source2>` spowoduje następujące krotek hello:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Dołącz do SPOŁECZNOŚCI przykład 2 z 3 źródeł:*  
  
- Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.  
  
- Let `<from_source2>` się zakres dokument odwołuje się do `input_alias1` i reprezentują zestawów:  
  
    {1, 2} dla`input_alias1 = A,`  
  
    {3} dla`input_alias1 = B,`  
  
    {4, 5} dla`input_alias1 = C,`  
  
- Let `<from_source3>` się zakres dokument odwołuje się do `input_alias2` i reprezentują zestawów:  
  
    {100, 200} dla`input_alias2 = 1,`  
  
    {300} dla`input_alias2 = 3,`  
  
- Witaj w klauzuli FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` spowoduje następujące krotek hello:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Brak spójnych kolekcji dla innych wartości `input_alias1`, `input_alias2`, dla których hello `<from_source3>` nie zwrócił żadnych wartości.  
  
*Dołącz do SPOŁECZNOŚCI przykład 3 z 3 źródeł:*  
  
- Let < from_source1 > można zakres kolekcji i reprezentują zestaw {A, B, C}.  
  
- Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.  
  
- Pozwól < from_source2 > można input_alias1 odwołującego się o zakresie dokumentu i reprezentują zestawów:  
  
    {1, 2} dla`input_alias1 = A,`  
  
    {3} dla`input_alias1 = B,`  
  
    {4, 5} dla`input_alias1 = C,`  
  
- Let `<from_source3>` wchodzą do zakresu zbyt`input_alias1` i reprezentują zestawów:  
  
    {100, 200} dla`input_alias2 = A,`  
  
    {300} dla`input_alias2 = C,`  
  
- Witaj w klauzuli FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` spowoduje następujące krotek hello:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), C, 4, 300, (C, 5, 300)  
  
> [!NOTE]
> Spowodowało to iloczyn wektorowy między `<from_source2>` i `<from_source3>` ponieważ oba są zakresami toohello tego samego `<from_source1>`.  Spowodowało to 4 (2 x 2) spójnych kolekcji o wartości A, 0 spójnych kolekcji o wartości B (1 x 0) i 2 (2 x 1) spójnych kolekcji o wartości C.  
  
**Zobacz też**  
  
 [Klauzula SELECT](#bk_select_query)  
  
##  <a name="bk_where_clause"></a>Klauzula WHERE  
 Określa warunek wyszukiwania hello dokumentów hello zwróconych przez zapytanie hello.  
  
 **Składnia**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Argumenty**  
  
-   `<filter_condition>`  
  
     Określa toobe warunku hello spełnia hello toobe dokumenty zwrócone.  
  
-   `<scalar_expression>`  
  
     Wyrażenie odpowiadające hello toobe wartość obliczana. Zobacz hello [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.  
  
 **Uwagi**  
  
 Aby hello toobe dokumentu zwracane wyrażenie określone jako warunek filtru musi zwrócić tootrue. Tylko wartość logiczną PRAWDA będzie spełniają warunek hello, wszelkie inne wartości: niezdefiniowana, null, wartość false, numer, tablicy lub obiekt nie spełniają warunek hello.  
  
##  <a name="bk_orderby_clause"></a>Klauzula ORDER BY  
 Określa sortowanie kolejność wyników zwróconych przez zapytanie hello hello.  
  
 **Składnia**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Argumenty**  
  
-   `<sort_specification>`  
  
     Określa właściwość lub wyrażenie, na którym zestawu wyników kwerendy hello toosort. Sortuj kolumny można określić jako alias nazwy lub kolumny.  
  
     Można określić wiele kolumn sortowania. Nazwy kolumn muszą być unikatowe. Sekwencja Hello hello sortowania kolumn w klauzuli ORDER BY hello definiuje hello organizacji hello sortowane zestawu wyników. To, że zestaw wyników hello są sortowane według hello pierwszą właściwością i następnie tej listy uporządkowanej są sortowane według właściwości drugi hello i tak dalej.  
  
     Witaj nazwy kolumn w klauzuli ORDER BY hello musi odpowiadać tooeither kolumny w hello wybierz kolumny z listy lub tooa zdefiniowany w tabeli określonej w klauzuli FROM hello bez żadnych niejednoznaczności.  
  
-   `<sort_expression>`  
  
     Określa jedną właściwość lub wyrażenie, na które zestawu wyników zapytania hello toosort.  
  
-   `<scalar_expression>`  
  
     Zobacz hello [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.  
  
-   `ASC | DESC`  
  
     Określa, że hello wartości w określonej kolumnie hello mają być sortowane w kolejności rosnącej lub malejącej. Sortuje ASC od wartości toohighest hello najniższej wartości. Sortuje DESC z najwyższą wartością toolowest wartości. ASC jest hello domyślny porządek sortowania. Wartości null są traktowane jako hello najmniejsze możliwe wartości.  
  
 **Uwagi**  
  
 Podczas hello gramatyki zapytań obsługuje wiele kolejność według właściwości, czasu wykonywania zapytania bazy danych Azure rozwiązania Cosmos hello obsługuje sortowanie, tylko jednej właściwości oraz tylko z nazwy właściwości, tj., nie dla właściwości obliczanej. Sortowanie wymaga również tego hello indeksowania zasad zawiera indeks zakresu dla właściwości hello i hello określony typ, z hello maksymalna dokładność. Zobacz toohello indeksowania dokumentacji zasad, aby uzyskać więcej informacji.  
  
##  <a name="bk_scalar_expressions"></a>Wyrażenia skalarne  
 Wyrażenie skalarne jest kombinacją symboli i operatory, które mogą być ocenione tooobtain pojedynczą wartość. Proste wyrażenia mogą być stałe, odwołań do właściwości, odwołania do elementu tablicy, odwołania do aliasu lub wywołania funkcji. Proste wyrażenia można łączyć przy użyciu operatorów wyrażenia.  
  
 Aby uzyskać szczegółowe informacje, na których wyrażenie skalarne może mieć wartości, zobacz [stałe](#bk_constants) sekcji.  
  
 **Składnia**  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 **Argumenty**  
  
-   `<constant>`  
  
     Reprezentuje wartość stałą. Zobacz [stałe](#bk_constants) sekcji, aby uzyskać szczegółowe informacje.  
  
-   `input_alias`  
  
     Reprezentuje wartość zdefiniowana przez hello `input_alias` wprowadzone w hello `FROM` klauzuli.  
    Ta wartość jest gwarantowana toonot można **Niezdefiniowany** —**Niezdefiniowany** wartości w danych wejściowych hello są pomijane.  
  
-   `<scalar_expression>.property_name`  
  
     Reprezentuje wartość hello właściwości obiektu. Jeśli właściwość hello nie istnieje lub odwołuje się do właściwości na wartość, która nie jest obiektem, a następnie hello wyrażenie zbyt**Niezdefiniowany** wartość.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Reprezentuje wartość hello właściwość o nazwie `property_name` lub element tablicy o indeksie `array_index` obiektu/tablicy. Jeśli indeks tablicy właściwości/hello nie istnieje lub indeks tablicy właściwości/hello odwołuje się do wartości, która nie jest Tablica obiektów /, następnie hello wynikiem wyrażenia jest wartość tooundefined.  
  
-   `unary_operator <scalar_expression>`  
  
     Reprezentuje operator, który jest stosowane tooa pojedyncza wartość. Zobacz [operatory](#bk_operators) sekcji, aby uzyskać szczegółowe informacje.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Reprezentuje operatora, który jest stosowane tootwo wartości. Zobacz [operatory](#bk_operators) sekcji, aby uzyskać szczegółowe informacje.  
  
-   `<scalar_function_expression>`  
  
     Reprezentuje wartość zdefiniowana przez wynik wywołania funkcji.  
  
-   `udf_scalar_function`  
  
     Nazwa użytkownika, powitalne zdefiniowane skalarną.  
  
-   `builtin_scalar_function`  
  
     Nazwa wbudowanej funkcji skalarnych hello.  
  
-   `<create_object_expression>`  
  
     Reprezentuje wartość uzyskany przez utworzenie nowego obiektu o określonej właściwości i ich wartości.  
  
-   `<create_array_expression>`  
  
     Reprezentuje wartość uzyskany przez utworzenie nowej tablicy z określonymi wartościami jako elementy  
  
-   `parameter_name`  
  
     Reprezentuje wartość hello określona nazwa parametru. Nazwy parametrów muszą mieć pojedynczy @ jako pierwszy znak hello.  
  
 **Uwagi**  
  
 Podczas wywoływania wbudowanych lub użytkownika definiowania funkcji skalarnych muszą być zdefiniowane wszystkie argumenty. Jeśli dowolny z argumentów hello jest niezdefiniowana, nie zostanie wywołana funkcja hello i hello wynik będzie niezdefiniowany.  
  
 Podczas tworzenia obiektu, dowolnej właściwości, która jest przypisana niezdefiniowana wartość zostanie pominięty i nie jest uwzględniony w hello utworzony obiekt.  
  
 Podczas tworzenia tablicy wartości elementu, który jest przypisany **Niezdefiniowany** wartość zostanie pominięty i nie jest uwzględniony w obiekcie hello utworzony. Hello obok zdefiniowany element tootake spowoduje jego miejsce w taki sposób, że tablica hello utworzone zostanie nie zostały pominięte indeksów.  
  
##  <a name="bk_operators"></a>Operatory  
 W tej sekcji opisano operatory hello obsługiwane. Każdy operator może być przypisany tooexactly jedną kategorię.  
  
 Zobacz **kategorii Operator** tabelę poniżej, aby uzyskać szczegółowe informacje dotyczące obsługi **Niezdefiniowany** wartości typu wymagania dotyczące obsługi z niezgodne typy wartości i wartości wejściowe.  
  
 **Operator kategorie:**  
  
|**Kategoria**|**Szczegóły**|  
|-|-|  
|**operacje arytmetyczne**|Operator oczekuje input(s) toobe numery. Dane wyjściowe również jest liczbą. Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub jest typu innego niż wynik numer, a następnie hello **Niezdefiniowany**.|  
|**bitowe**|Operator oczekuje input(s) toobe 32-bitowej liczby całkowitej ze znakiem numery. Dane wyjściowe jest również 32-bitowa liczba całkowita.<br /><br /> Zostanie zaokrąglony żadnej wartości niebędące liczbami całkowitymi. Wartość dodatnią zostaną zaokrąglone w dół, ujemne wartości zaokrąglona w górę.<br /><br /> Każdą wartość, która znajduje się poza zakresem 32-bitową liczbę całkowitą hello zostanie przekonwertowany, wykonując ostatnich 32 bity jego dwa w notacji uzupełnienia.<br /><br /> Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub wpisz inne niż numer, a następnie wynik hello jest **Niezdefiniowany**.<br /><br /> **Uwaga:** hello powyżej zachowanie jest zgodne z zachowanie bitowy operator w JavaScript.|  
|**logiczne**|Operator oczekuje input(s) toobe Boolean(s). Dane wyjściowe również jest wartością logiczną.<br />Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub typu, innego niż Boolean, hello wynikiem będzie **Niezdefiniowany**.|  
|**Porównanie**|Operator oczekuje input(s) hello toohave sam typu i nie jest niezdefiniowany. Dane wyjściowe jest wartością logiczną.<br /><br /> Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub hello dane wejściowe mają różne typy, a następnie wynik hello jest **Niezdefiniowany**.<br /><br /> Zobacz **porządkowanie wartości do porównania** tabeli dla wartości kolejności szczegóły.|  
|**ciąg**|Operator oczekuje input(s) toobe ciągi. Dane wyjściowe również jest ciągiem.<br />Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub jest typu innego niż wynik ciągu, a następnie hello **Niezdefiniowany**.|  
  
 **Operatory jednoargumentowe:**  
  
|**Nazwa**|**Operator**|**Szczegóły**|  
|-|-|-|  
|**operacje arytmetyczne**|+<br /><br /> -|Zwraca wartość liczbową hello.<br /><br /> Bitową negację. Zwraca zanegowane wartość liczbową.|  
|**bitowe**|~|Uzupełnienie tych. Zwraca uzupełnienie wartość liczbową.|  
|**Logiczne**|**NIE**|Negacja. Zwraca zanegowane wartość logiczna.|  
  
 **Operatory binarne:**  
  
|**Nazwa**|**Operator**|**Szczegóły**|  
|-|-|-|  
|**operacje arytmetyczne**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Dodatek.<br /><br /> Odejmowanie.<br /><br /> Mnożenia.<br /><br /> Podział.<br /><br /> Modulacji.|  
|**bitowe**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|Wartość logiczną lub.<br /><br /> Bitowe koniunkcji binarnej.<br /><br /> Iloczynu bitowego XOR.<br /><br /> Przesunięcia w lewo.<br /><br /> Przesunięcia w prawo.<br /><br /> Przesunięcia w prawo wypełnienia zero.|  
|**logiczne**|**I**<br /><br /> **LUB**|Połączenie logiczne. Zwraca **true** Jeśli oba argumenty mają **true**, zwraca **false** inaczej.<br /><br /> Połączenie logiczne. Zwraca **true** Jeśli oba argumenty mają **true**, zwraca **false** inaczej.|  
|**Porównanie**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Równa się. Zwraca **true** argumenty są takie same, funkcja zwraca **false** inaczej.<br /><br /> Nie równa się. Zwraca **true** argumenty nie są równe, zwraca **false** inaczej.<br /><br /> Większa. Zwraca **true** Jeśli pierwszy argument jest większy niż drugi hello, **false** inaczej.<br /><br /> Większe lub równe. Zwraca **true** Jeśli pierwszy argument jest większa niż lub równa toohello drugi z nich, zwróć **false** inaczej.<br /><br /> Poniżej. Zwraca **true** Jeśli pierwszy argument jest mniejszy niż drugi Witaj, zwróć **false** inaczej.<br /><br /> Mniejsze niż lub równe. Zwraca **true** Jeśli pierwszy argument jest mniejsza lub równa toohello drugie jedną zwracany **false** inaczej.<br /><br /> Połączenie. Zwraca hello drugi argument, jeśli pierwszy argument hello jest **Niezdefiniowany** wartość.|  
|**Ciąg**|**&#124;&#124;**|Łączenie. Zwraca złączeniem oba argumenty.|  
  
 **Operatory trzyargumentowe:**  
  
|Operator trójargumentowy|?|Zwraca hello drugi argument, jeśli pierwszy argument hello zbyt**true**; w przeciwnym razie zwraca hello trzeci argument.|  
|-|-|-|  
  
 **Kolejność wartości do porównania**  
  
|**Typ**|**Kolejność wartości**|  
|-|-|  
|**Niezdefiniowana**|Nie można porównywać.|  
|**Wartość null**|Pojedyncza wartość: **wartości null**|  
|**Numer**|Liczba rzeczywista fizycznych.<br /><br /> Wartości nieskończoności ujemnej jest mniejszy niż inne wartość liczbową.<br /><br /> Dodatnia wartość Infinity jest większy niż inne wartość liczbową. **NaN** wartość nie jest on porównywalny. Porównanie z **NaN** spowoduje **Niezdefiniowany** wartość.|  
|**Ciąg**|Kolejność lexicographical.|  
|**Tablica**|Nie określania kolejności, ale słuszne.|  
|**Obiekt**|Nie określania kolejności, ale słuszne.|  
  
 **Uwagi**  
  
 W usłudze Azure DB rozwiązania Cosmos hello typy wartości, często nie są znane, do momentu rzeczywistości pobrania z bazy danych hello. Kolejność toosupport wydajność wykonywania zapytań większość operatorów hello ma wymagania typu strict. Operatory samodzielnie nie wykonuj również niejawną konwersję.  
  
 Oznacza to, że zapytanie, takich jak: Wybierz * z katalogu głównego r WHERE r.Age = 21 zwróci tylko te dokumenty z właściwością liczby równy toohello wieku 21. Dokumenty z właściwości wieku równy toohello ciąg "21" lub ciąg hello "0021", nie będzie odpowiadała jako wyrażenie hello "21" = 21 ocenia tooundefined. Umożliwia to lepsze wykorzystanie indeksów, ponieważ wyszukiwanie hello określonej wartości (np. numer 21) jest szybsze niż wyszukiwanie nieokreśloną liczbę potencjalnych (tj. liczba 21 lub ciągi "21", "021", "21.0"...). To różni się od sposobu JavaScript ocenia operatory na wartości różnych typów.  
  
 **Porównanie i równości obiektów i tablic**  
  
 Porównywanie tablicy lub obiekt wartości przy użyciu operatorów zakresu (>, > =, <, < =) spowoduje niezdefiniowana, ponieważ nie ma nie kolejności zdefiniowane dla obiektu ani tablicy wartości. Jednak przy użyciu operatorów równości i nierówności (=,! =, <>) jest obsługiwana i będzie można porównać wartości strukturę.  
  
 Tablice są takie same, jeśli obie tablice mają tę samą liczbę elementów, a elementy w pozycji dopasowania również są takie same. Jeśli porównanie jakiejkolwiek parze elementów powoduje Niezdefiniowany, hello wynik porównania tablicy nie jest zdefiniowana.  
  
 Obiekty są takie same, jeśli oba obiekty mają takie same właściwości zdefiniowane, a także są takie same wartości dopasowania właściwości. Jeśli porównanie każdej pary wartości właściwości powoduje Niezdefiniowany, hello wynik porównania obiektu jest zdefiniowana.  
  
##  <a name="bk_constants"></a>Stałe  
 Stała, znana także jako literału lub wartość skalarną, to symbol, który reprezentuje wartość określonych danych. format Hello stałej zależy od typu danych hello hello wartość, która reprezentuje.  
  
 **Obsługiwane typy skalarne danych:**  
  
|**Typ**|**Kolejność wartości**|  
|-|-|  
|**Niezdefiniowana**|Pojedyncza wartość: **niezdefiniowane**|  
|**Wartość null**|Pojedyncza wartość: **wartości null**|  
|**Wartość logiczna**|Wartości: **false**, **true**.|  
|**Numer**|Liczba podwójnej precyzji liczb zmiennoprzecinkowych, IEEE-754 standardowa.|  
|**Ciąg**|Sekwencja zero lub więcej znaków Unicode. Ciągi, musi być ujęty w pojedynczym lub podwójnym cudzysłowie.|  
|**Tablica**|Sekwencja zero lub więcej elementów. Każdy element może być wartością dowolnego typu danych skalarnych, z wyjątkiem Undefined.|  
|**Obiekt**|Nieuporządkowaną zestaw par nazwa/wartość zero lub więcej. Nazwa jest ciągiem Unicode, wartość może być dowolnego typu danych skalarnych, z wyjątkiem **niezdefiniowane**.|  
  
 **Składnia**  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 **Argumenty**  
  
1.  `<undefined_constant>; undefined`  
  
     Reprezentuje niezdefiniowana wartość typu Undefined.  
  
2.  `<null_constant>; null`  
  
     Reprezentuje **null** wartości typu **Null**.  
  
3.  `<boolean_constant>`  
  
     Reprezentuje stała typu Boolean.  
  
4.  `false`  
  
     Reprezentuje **false** wartość typu Boolean.  
  
5.  `true`  
  
     Reprezentuje **true** wartość typu Boolean.  
  
6.  `<number_constant>`  
  
     Reprezentuje stałą.  
  
7.  `decimal_literal`  
  
     Literałów dziesiętnych są liczbami reprezentowanej przy użyciu notacji dziesiętnej lub wykładniczej.  
  
8.  `hexadecimal_literal`  
  
     Literały szesnastkowe są przedstawiane za pomocą prefiks '0 x' następuje co najmniej jedną cyfrę szesnastkową liczby.  
  
9. `<string_constant>`  
  
     Reprezentuje stałą typu String.  
  
10. `string _literal`  
  
     Literały ciągu są reprezentowane przez sekwencję zero lub więcej znaków Unicode lub sekwencji unikowych ciągów Unicode. Literały ciągu są ujęte w apostrofy (apostrof: ") lub podwójne cudzysłowy (cudzysłów:").  
  
 Dopuszczalne są następujące sekwencje unikowe:  
  
|**Sekwencja specjalna**|**Opis**|**Znak Unicode**|  
|-|-|-|  
|\\'|apostrof (')|U + 0027|  
|\\"|znak cudzysłowu (")|U + 0022|  
|\\\|Odwrotna kreska ułamkowa (\\)|U + 005C|  
|\\/|kreska ułamkowa (/)|U + 002F|  
|\b|BACKSPACE|U + 0008|  
|\f|Wysuw strony|U + 000C|  
|\n|wysuwu wiersza|U + 000A|  
|\r|Powrót karetki|U + 000D|  
|\t|Karta|U + 0009|  
|\uXXXX|Znak Unicode, zdefiniowane przez 4 cyfr szesnastkowych.|U + XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a>Wskazówki dotyczące wydajności kwerendy  
 Aby toobe zapytanie, wykonywane wydajnie dla dużych kolekcji powinien on używać filtrów, które mogą być przekazywane za pośrednictwem jednego lub kilku indeksów.  
  
 Indeks wyszukiwania będzie mogła zostać usunięta Hello następujące filtry:  
  
-   Za pomocą operatora równości (=) wyrażenie ścieżki dokumentu i stałą.  
  
-   Operatory zakresu (<, \<=, >, > =) z wyrażenie ścieżki dokumentu i number — stałe.  
  
-   Wyrażenie ścieżki dokumentu oznacza dowolne wyrażenie, które identyfikuje ścieżkę stałej w dokumentach hello z hello odwołuje się do bazy danych kolekcji.  
  
 **Wyrażenie ścieżki dokumentu**  
  
 Wyrażenia ścieżki dokumentu są wyrażenia który ścieżki właściwości lub tablicy oceniających indeksatora za pośrednictwem dokumentu pochodzące z bazy danych kolekcji dokumentów. Ta ścieżka może być używane tooidentify lokalizację hello wartości filtru bezpośrednio z poziomu hello dokumentów w kolekcji z bazy danych hello.  
  
 Aby toobe wyrażenie traktowane jako wyrażenie ścieżki dokumentu powinno:  
  
1.  Odwołanie hello kolekcji głównego bezpośrednio.  
  
2.  Indeksator odwołanie do właściwości lub stała tablicy niektóre wyrażenia ścieżki dokumentu  
  
3.  Odwołanie alias, który reprezentuje wyrażenie ścieżki niektórych dokumentów.  
  
     **Konwencje składni**  
  
     Witaj w poniższej tabeli opisano składnię toodescribe używane konwencje hello w odwołaniu do hello język zapytań usługi DocumentDB interfejsu API.  
  
    |**Konwencja**|**Używany do**|  
    |-|-|    
    |WIELKIE LITERY|Słowa kluczowe bez uwzględniania wielkości liter.|  
    |małe litery|Słowa kluczowe z uwzględnieniem wielkości liter.|  
    |\<nonterminal >|Nonterminal, definiowane osobno.|  
    |\<nonterminal >:: =|Definicja składni hello nonterminal.|  
    |other_terminal|Terminali (token) opisano szczegółowo w wyrazy.|  
    |Identyfikator|Identyfikator. Umożliwia następujące znaki: a-z A-Z 0-9 _First znak nie może być cyfrą.|  
    |"string"|Ciąg w cudzysłowie. Umożliwia dowolny prawidłowy ciąg. Zobacz opis literał.|  
    |"symbol"|Literał symbol, który jest częścią hello składni.|  
    |&#124; (pionowa kreska)|Alternatywy dla elementy składni. Można użyć tylko jednej z określonych elementów hello.|  
    |/(brackets)]|Nawiasy kwadratowe powinno być jeden lub więcej elementów opcjonalnych.|  
    |[,.. .n]|Wskazuje, że hello poprzedzających elementu może być powtarzane n liczbę razy. wystąpienia Hello są oddzielone przecinkami.|  
    |[.. .n]|Wskazuje, że hello poprzedzających elementu może być powtarzane n liczbę razy. wystąpienia Hello są rozdzielane puste wartości.|  
  
##  <a name="bk_built_in_functions"></a>Funkcje wbudowane  
 Azure DB rozwiązania Cosmos udostępnia wiele wbudowanych funkcji SQL. Poniżej wymieniono kategorie Hello funkcji wbudowanych.  
  
|Funkcja|Opis|  
|--------------|-----------------|  
|[Funkcje matematyczne](#bk_mathematical_functions)|Witaj funkcje matematyczne każdego wykonywanie obliczeń, zwykle oparte na wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową.|  
|[Typ funkcji sprawdzania](#bk_type_checking_functions)|Sprawdzanie, czy funkcje typu Hello pozwalają toocheck hello typ wyrażenia w obrębie zapytania SQL.|  
|[Funkcje ciągów](#bk_string_functions)|Funkcje ciągów Hello wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna.|  
|[Funkcje tablicy](#bk_array_functions)|Funkcje tablicy Hello wykonywać operacji na tablicy wartości wejściowej i przywracać liczbowych, wartość logiczną lub tablicy.|  
|[Funkcje przestrzenne](#bk_spatial_functions)|Funkcje przestrzenne Hello wykonania operacji na wartości wejściowej obiektu przestrzennego i zwracać wartość liczbowa lub wartość logiczna.|  
  
###  <a name="bk_mathematical_functions"></a>Funkcje matematyczne  
 Witaj następujące funkcje wykonywanie obliczeń, zwykle oparte na wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[LIMITU](#bk_ceiling)|  
|[COS](#bk_cos)|[KOT](#bk_cot)|[STOPNI](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[DZIENNIK](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[ZASILANIA](#bk_power)|  
|[WARTOŚĆ W RADIANACH](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[KWADRATOWE](#bk_square)|[ZALOGUJ SIĘ](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC —](#bk_trunc)||  
  
####  <a name="bk_abs"></a>ABS  
 Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe.  
  
 **Składnia**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład przedstawia wyniki hello przy użyciu funkcji hello ABS na trzy różne liczby.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a>ACOS  
 Zwraca hello kąt w radianach, którego cosinus jest hello określonego wyrażenia liczbowego. Skrót cosinus.  
  
 **Składnia**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello ACOS-1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a>ASIN  
 Zwraca hello kąt w radianach, którego sinusem jest dana hello określony wyrażenia liczbowego. Jest to również sinus.  
  
 **Składnia**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello ASIN-1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a>ATAN  
 Zwraca hello kąt w radianach, którego tangens jest hello określony wyrażenia liczbowego. Jest to również tangens.  
  
 **Składnia**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Poniższy przykład, że zwraca hello ATAN hello Hello określona wartość.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a>ATN2  
 Zwraca wartość główną hello hello arcus tangens y / x, wyrażone w radianach.  
  
 **Składnia**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład oblicza hello ATN2 dla hello określony x i y składników.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a>LIMITU  
 Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego.  
  
 **Składnia**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Hello poniższy przykład przedstawia dodatnią liczbowe, ujemna, i wartości zerowe z hello limitu funkcji.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a>COS  
 Zwraca hello trygonometryczne cosinus hello określony kąt w radianach, w hello określone wyrażenie.  
  
 **Składnia**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Poniższy przykład Hello oblicza hello COS hello określone kąta.  
  
```  
SELECT COS(14.78)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a>KOT  
 Zwraca hello trygonometryczne cotangens hello określony kąt w radianach, w hello określonego wyrażenia liczbowego.  
  
 **Składnia**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Poniższy przykład Hello oblicza hello KOT hello podanemu kątowi.  
  
```  
SELECT COT(124.1332)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a>STOPNI  
 Zwraca hello odpowiadający mu kąt w stopniach dla kąta określonego w radianach.  
  
 **Składnia**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello liczba stopni w kąta PI/2 radianów.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a>FLOOR  
 Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe.  
  
 **Składnia**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Hello poniższy przykład przedstawia dodatnią liczbowe, ujemna, i wartości zerowe z hello FLOOR — funkcja.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a>EXP  
 Zwraca hello wykładniczej wartość hello określona wyrażenia liczbowego.  
  
 **Składnia**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Uwagi**  
  
 Stała Hello **e** (2.718281...), jest hello podstawowej podstawę logarytmu naturalnego.  
  
 Witaj wykładnik liczby jest stała hello **e** wywoływane potęgi toohello liczba hello. Na przykład EXP(1.0) = e ^ 1.0 = 2.71828182845905 i EXP(10) = e ^ 10 = 22026.4657948067.  
  
 Hello wykładniczej z hello logarytm naturalny liczby jest liczba hello, sama: EXP (dziennik (n)) = n. I logarytm naturalny hello hello wykładnicza liczby jest liczba hello, sama: dziennika (EXP (n)) = n.  
  
 **Przykłady**  
  
 Witaj poniższy przykład deklaruje zmienną i zwraca wartość wykładniczej hello hello określonej zmiennej (10).  
  
```  
SELECT EXP(10)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Witaj poniższy przykład zwraca hello wykładniczej wartości logarytmu naturalnego hello 20 i logarytm naturalny hello hello wykładniczej 20. Ponieważ te funkcje są funkcje odwrócone siebie, zwracana wartość hello z zaokrąglania zmiennoprzecinkowa matematyczne w obu przypadkach to 20.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a>DZIENNIK  
 Zwraca logarytm naturalny hello hello określone wyrażenie liczbowe.  
  
 **Składnia**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
-   `base`  
  
     Opcjonalny argument numeryczny, która ustawia hello jest podstawą logarytmu hello.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Uwagi**  
  
 Domyślnie LOG() Zwraca logarytm naturalny hello. Opcjonalny parametr podstawowego hello można zmienić base hello hello logarytm tooanother wartości.  
  
 logarytm naturalny Hello jest podstawowy toohello logarytm hello **e**, gdzie **e** jest nieracjonalnej stałej too2.718281828 przybliżeniu równe.  
  
 logarytm naturalny Hello hello wykładnicza liczby jest liczba hello, sama: dziennika (EXP (n)) = n. A hello wykładniczej z hello logarytm naturalny liczby jest liczbą hello, sama: EXP (dziennik (n)) = n.  
  
 **Przykłady**  
  
 Witaj poniższy przykład deklaruje zmienną i zwraca wartość logarytmu hello hello określonej zmiennej (10).  
  
```  
SELECT LOG(10)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Witaj poniższy przykład oblicza hello dziennika dla wykładnik hello liczby.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a>LOG10  
 Zwraca logarytm base 10 hello hello określone wyrażenie liczbowe.  
  
 **Składnia**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Uwagi**  
  
 Witaj LOG10 i funkcje zasilania są tooone odwrotnie pokrewne innego. Na przykład 10 ^ LOG10(n) = n.  
  
 **Przykłady**  
  
 Witaj poniższy przykład deklaruje zmienną i zwraca wartość LOG10 hello hello określonej zmiennej (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a>PI  
 Zwraca hello stałą wartość PI.  
  
 **Składnia**  
  
```  
PI ()  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello wartość PI.  
  
```  
SELECT PI()  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a>ZASILANIA  
 Zwraca hello wartość hello określone wyrażenie toohello określony zasilania.  
  
 **Składnia**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
-   `y`  
  
     Jest hello zasilania toowhich tooraise `numeric_expression`.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Hello poniższy przykład pokazuje, zwiększenie numeru zasilania toohello 3 (hello modułu liczby hello).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a>WARTOŚĆ W RADIANACH  
 Zwraca wartość w radianach, po wprowadzeniu w stopniach, wyrażenia liczbowego.  
  
 **Składnia**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład przyjmuje jako dane wejściowe kilka kąty i zwraca odpowiednimi wartościami radianach.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a>ROUND  
 Zwraca wartość liczbową zaokrąglony toohello najbliższej liczby całkowitej wartości.  
  
 **Składnia**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zaokrągla hello następującej liczby dodatnie i ujemne toohello najbliższej liczby całkowitej.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a>ZALOGUJ SIĘ  
 Zwraca hello plus (+ 1) (0), lub znakiem minus (-1) z hello określone wyrażenie liczbowe.  
  
 **Składnia**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello znak wartości liczb z too2-2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a>SIN  
 Zwraca hello trygonometryczne sinus hello określony kąt w radianach, w hello określone wyrażenie.  
  
 **Składnia**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Poniższy przykład Hello oblicza hello SINUS określonego kąta hello.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a>SQRT  
 Zwraca pierwiastek kwadratowy hello hello określono wartość liczbową.  
  
 **Składnia**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca pierwiastków kwadratowych hello liczb od 1 do 3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a>KWADRATOWE  
 Zwraca hello kwadratowy z hello określono wartość liczbową.  
  
 **Składnia**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello kwadratów liczb od 1 do 3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a>TAN  
 Zwraca tangens hello hello określony kąt w radianach, w hello określone wyrażenie.  
  
 **Składnia**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład oblicza tangens hello (PI) / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a>TRUNC —  
 Zwraca wartość liczbową skróconą toohello najbliższą wartość całkowitą.  
  
 **Składnia**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Argumenty**  
  
-   `numeric_expression`  
  
     To wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Poniższy przykład Hello obcina hello następującej liczby dodatnie i ujemne toohello najbliższej liczby całkowitej wartości.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a>Typ funkcji sprawdzania  
 Hello następujące funkcje obsługi typu sprawdzanie względem wartości wejściowe, a każdy zwracać wartość logiczną.  
  
||||  
|-|-|-|  
|[IS_ARRAY —](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT —](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a>IS_ARRAY —  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest tablicą.  
  
 **Składnia**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg, wartość null, obiekt, tablicy i niezdefiniowane typów za pomocą hello is_array — funkcja.  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a>IS_BOOL  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest wartością logiczną.  
  
 **Składnia**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_BOOL funkcji.  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a>IS_DEFINED  
 Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość.  
  
 **Składnia**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 powitania po przykład sprawdza obecność hello właściwości w hello określony dokument JSON. Witaj najpierw zwraca wartość true, ponieważ "a" jest obecny, ale hello drugi zwraca wartość false, ponieważ nie ma "b".  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a>IS_NULL  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie ma wartość null.  
  
 **Składnia**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_NULL funkcji.  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a>IS_NUMBER  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest liczbą.  
  
 **Składnia**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_NULL funkcji.  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a>IS_OBJECT —  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest obiektem JSON.  
  
 **Składnia**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg, wartość null, obiekt, tablicy i niezdefiniowane typów za pomocą hello is_object — funkcja.  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a>IS_PRIMITIVE  
 Zwraca wartość logiczną wskazującą, czy określony typ hello hello wyrażenie jest typu pierwotnego (string, Boolean, liczbowa lub wartość null).  
  
 **Składnia**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_PRIMITIVE funkcji.  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a>IS_STRING  
 Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest ciągiem.  
  
 **Składnia**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Argumenty**  
  
-   `expression`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_STRING funkcji.  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a>Funkcje ciągów  
 Witaj następujące funkcje skalarne wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[ZAWIERA](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[PO LEWEJ](#bk_left)|[DŁUGOŚĆ](#bk_length)|  
|[NIŻSZE](#bk_lower)|[PRZYTP](#bk_ltrim)|[ZAMIEŃ](#bk_replace)|  
|[REPLIKUJ](#bk_replicate)|[REVERSE](#bk_reverse)|[PRAWO](#bk_right)|  
|[PRZYTK](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[GÓRNY](#bk_upper)|||  
  
####  <a name="bk_concat"></a>CONCAT  
 Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu.  
  
 **Składnia**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 powitania po przykład zwraca ciąg hello połączonych hello określone wartości.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a>ZAWIERA  
 Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello.  
  
 **Składnia**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Witaj poniższy przykład sprawdza, czy "abc" zawiera "ab" a "d".  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a>ENDSWITH  
 Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi.  
  
 **Składnia**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca powitalne "abc" kończy się wyrazem "b" i "bc".  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a>INDEX_OF  
 Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello.  
  
 **Składnia**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca indeks hello różnych podciągów wewnątrz "abc".  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a>PO LEWEJ  
 Zwraca hello lewej części ciągu z hello określona liczba znaków.  
  
 **Składnia**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
-   `num_expr`  
  
     Jest dowolne prawidłowe wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello lewej części "abc" dla różnych wartości długości.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a>DŁUGOŚĆ  
 Witaj zwraca liczbę znaków hello określone wyrażenie ciągu.  
  
 **Składnia**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello długość ciągu.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a>NIŻSZE  
 Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę.  
  
 **Składnia**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toouse małe w zapytaniu.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a>PRZYTP  
 Zwraca wyrażenie ciągu, po usuwa spacje wiodące.  
  
 **Składnia**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toouse LTRIM w zapytaniu.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a>ZAMIEŃ  
 Zamienia wszystkie wystąpienia określonej wartości ciągu na inną wartość ciągu.  
  
 **Składnia**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład pokazuje, jak zastąpić toouse w zapytaniu.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a>REPLIKOWANIE  
 Wartość ciągu jest powtarzany określoną liczbę razy.  
  
 **Składnia**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
-   `num_expr`  
  
     Jest dowolne prawidłowe wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład przedstawia sposób REPLIKOWANIA toouse w zapytaniu.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a>REVERSE  
 Zwraca hello odwrotna kolejność wartość ciągu.  
  
 **Składnia**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład pokazuje, jak toouse wstecznego w zapytaniu.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a>PRAWO  
 Zwraca hello prawej części ciągu z hello określona liczba znaków.  
  
 **Składnia**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
-   `num_expr`  
  
     Jest dowolne prawidłowe wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca hello prawa część "abc" dla różnych wartości długości.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a>PRZYTK  
 Zwraca wyrażenie ciągu, po usuwa spacje końcowe.  
  
 **Składnia**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toouse RTRIM w zapytaniu.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a>STARTSWITH  
 Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello rozpoczyna się od hello drugi.  
  
 **Składnia**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 Witaj poniższy przykład sprawdza, czy hello ciągu "abc" rozpoczyna się od ciągu "b" i "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a>SUBSTRING  
 Zwraca część wyrażenia ciągu, zaczynając od hello określono znaku na pozycji liczony od zera i kontynuuje toohello określone długości lub toohello końca ciągu hello.  
  
 **Składnia**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
-   `num_expr`  
  
     Jest dowolne prawidłowe wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 Witaj poniższy przykład zwraca podciąg hello "abc" począwszy od 1 i o długości 1 znak.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a>GÓRNY  
 Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę.  
  
 **Składnia**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Argumenty**  
  
-   `str_expr`  
  
     Jest dowolne wyrażenie prawidłowy ciąg.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie ciągu.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toouse górna w kwerendzie  
  
```  
SELECT UPPER("Abc")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a>Funkcje tablicy  
 następujące funkcje skalarne Hello wykonania operacji na tablicy wartości wejściowej i powrotu liczbowego, wartość logiczną lub tablicy  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a>ARRAY_CONCAT  
 Zwraca tablicę, która jest wynikiem hello łączenie dwóch lub więcej wartości tablicy.  
  
 **Składnia**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Argumenty**  
  
-   `arr_expr`  
  
     Jest dowolne wyrażenie prawidłowy tablicy.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie tablicy.  
  
 **Przykłady**  
  
 Witaj następujący przykład sposobu tooconcatenate dwóch stałych.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a>ARRAY_CONTAINS  
 Zwraca wartość typu Boolean wskazującą, czy tablica hello zawiera hello określona wartość.  
  
 **Składnia**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Argumenty**  
  
-   `arr_expr`  
  
     Jest dowolne wyrażenie prawidłowy tablicy.  
  
-   `expr`  
  
     Jest dowolne prawidłowe wyrażenie.  
  
 **Zwracane typy**  
  
 Zwraca wartość logiczną.  
  
 **Przykłady**  
  
 Poniższy przykład sposobu Hello toocheck członkostwa w tablicy przy użyciu ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a>ARRAY_LENGTH  
 Zwraca numer hello elementów hello określone wyrażenie tablicy.  
  
 **Składnia**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Argumenty**  
  
-   `arr_expr`  
  
     Jest dowolne wyrażenie prawidłowy tablicy.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego.  
  
 **Przykłady**  
  
 następujący przykład Witaj, jak tooget hello długość tablicy przy użyciu ARRAY_LENGTH.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a>ARRAY_SLICE  
 Zwraca część wyrażenie tablicy.
  
 **Składnia**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumenty**  
  
-   `arr_expr`  
  
     Jest dowolne wyrażenie prawidłowy tablicy.  
  
-   `num_expr`  
  
     Jest dowolne prawidłowe wyrażenie liczbowe.  
  
 **Zwracane typy**  
  
 Zwraca wartość logiczną.  
  
 **Przykłady**  
  
 Poniższy przykład sposobu Hello tooget część tablicy przy użyciu ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a>Funkcje przestrzenne  
 Witaj następujące funkcje skalarne wykonania operacji na wartości wejściowej obiektu przestrzennego i zwracać wartość liczbowa lub wartość logiczna.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a>ST_DISTANCE  
 Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.  
  
 **Składnia**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenty**  
  
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.  
  
 **Zwracane typy**  
  
 Zwraca wartość wyrażenia liczbowego zawierający hello odległości. To wymaganie jest wyrażone w liczników dla systemu odniesienia hello domyślne.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak tooreturn wszystkie dokumenty rodziny, które są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a>ST_WITHIN  
 Zwraca wyrażenie Boolean wskazującą, czy hello GeoJSON (punkt, wielokąta lub LineString) określony obiekt w pierwszym argumencie hello mieści hello GeoJSON (punkt, wielokąta lub LineString) hello drugi argument.  
  
 **Składnia**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenty**  
  
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.  
 
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.  
  
 **Zwracane typy**  
  
 Zwraca wartość logiczną.  
  
 **Przykłady**  
  
 Witaj poniższy przykład pokazuje, jak toofind rodziny wszystkich dokumentów w ramach przy użyciu ST_WITHIN wielokąta.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a>ST_INTERSECTS  
 Zwraca wartość wskazującą, czy hello GeoJSON (punkt, wielokąta lub LineString) określony obiekt w pierwszym argumencie hello przecina hello GeoJSON (punkt, wielokąta lub LineString) w hello drugi argument wyrażenia logicznego.  
  
 **Składnia**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumenty**  
  
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.  
 
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.  
  
 **Zwracane typy**  
  
 Zwraca wartość logiczną.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toofind wszystkich obszarów, które przecina z hello podany wielokąta.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a>ST_ISVALID  
 Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.  
  
 **Składnia**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumenty**  
  
-   `spatial_expr`  
  
     Jest dowolne prawidłowe wyrażenie GeoJSON punktu wielokąta i LineString.  
  
 **Zwracane typy**  
  
 Zwraca wyrażenie logiczne.  
  
 **Przykłady**  
  
 powitania po przykładzie pokazano, jak toocheck, gdy punkt jest nieprawidłowy, przy użyciu ST_VALID.  
  
 Na przykład ten punkt ma wartość szerokości geograficznej, który nie jest prawidłowy zakres wartości [-90, 90] hello, więc hello zapytanie zwraca wartość false.  
  
 W przypadku wielokątów hello GeoJSON specyfikacji wymaga hello ostatnią parę współrzędnych podane powinien hello sam jako pierwszy, toocreate hello zamknięty kształt. Punktów w wielokąta muszą być określone w kolejności przeciwnie do ruchu wskazówek zegara. Wielokąt określony w kolejności zegara reprezentuje odwrotność hello hello regionu w niej.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED  
 Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.  
  
 **Składnia**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumenty**  
  
-   `spatial_expr`  
  
     Jest dowolne GeoJSON prawidłowe wyrażenie punktu lub wielokąta.  
  
 **Zwracane typy**  
  
 Zwraca wartość JSON zawierający wartość logiczną w przypadku hello określony punkt GeoJSON lub wyrażenie wielokąta jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.  
  
 **Przykłady**  
  
 Poniższy przykład sposobu Hello ważności toocheck (ze szczegółami) przy użyciu ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Oto hello zestawu wyników.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Następne kroki  
 [Składnia SQL i kwerendy SQL dla bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md)   
 [Dokumentację platformy Azure DB rozwiązania Cosmos](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
