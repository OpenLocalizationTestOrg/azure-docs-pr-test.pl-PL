---
<span data-ttu-id="650b0-101">title: aaa "interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB: składnia SQL | Opis elementu Microsoft Docs": odwołanie dokumentacji hello język zapytań SQL interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="650b0-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="650b0-102">usługi: Autor db rozwiązania cosmos: Menedżera mimig1: Edytor jhubbard: mimig documentationcenter: "</span><span class="sxs-lookup"><span data-stu-id="650b0-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="650b0-103">MS.AssetID: ms.service: ms.workload db rozwiązania cosmos: ms.tgt_pltfrm usług danych: na ms.devlang: na ms.topic: odwołanie ms.date: ms.author 2017-06/13: mimig</span><span class="sxs-lookup"><span data-stu-id="650b0-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="650b0-104">Azure DocumentDB rozwiązania Cosmos DB interfejsu API: Odwołania do składni SQL</span><span class="sxs-lookup"><span data-stu-id="650b0-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="650b0-105">Hello interfejsu API Azure rozwiązania Cosmos bazy danych DocumentDB obsługuje tworzenie zapytań dla dokumentów za pomocą znanych SQL (Structured Query Language) jak gramatyki przez hierarchiczna dokumentów JSON bez konieczności jawnego schematu lub tworzenia indeksów pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="650b0-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="650b0-106">Ten temat zawiera dokumentację referencyjną dla hello język zapytań SQL usługi DocumentDB interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="650b0-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="650b0-107">Aby uzyskać wskazówki hello język zapytań SQL usługi DocumentDB interfejsu API, zobacz [kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="650b0-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="650b0-108">Również zachęcamy toovisit hello [Plac zabaw dla zapytań](http://www.documentdb.com/sql/demo) gdzie spróbuj bazy danych rozwiązania Cosmos Azure i wykonywania kwerend SQL do naszego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="650b0-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="650b0-109">Zapytanie SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-109">SELECT query</span></span>  
<span data-ttu-id="650b0-110">Pobiera dokumentów JSON z hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="650b0-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="650b0-111">Obsługuje oceny wyrażenia, projekcji, filtrowania i tworzy sprzężenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="650b0-112">konwencje Hello opisujących hello instrukcji "SELECT" wyszczególniono w hello sekcji konwencje składni.</span><span class="sxs-lookup"><span data-stu-id="650b0-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="650b0-113">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="650b0-114">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-114">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-115">Zobacz następujące sekcje, aby uzyskać szczegółowe informacje na każdej klauzuli:</span><span class="sxs-lookup"><span data-stu-id="650b0-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="650b0-116">Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="650b0-117">Klauzula FROM</span><span class="sxs-lookup"><span data-stu-id="650b0-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="650b0-118">Klauzula WHERE</span><span class="sxs-lookup"><span data-stu-id="650b0-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="650b0-119">Klauzula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="650b0-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="650b0-120">klauzule Hello w instrukcji SELECT hello muszą być uporządkowane, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="650b0-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="650b0-121">Jeden z hello opcjonalna klauzula można pominąć.</span><span class="sxs-lookup"><span data-stu-id="650b0-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="650b0-122">Jednak w przypadku używania klauzule opcjonalne muszą występować w odpowiedniej kolejności hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="650b0-123">**Logiczna kolejność przetwarzania hello instrukcji SELECT**</span><span class="sxs-lookup"><span data-stu-id="650b0-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="650b0-124">Witaj kolejność przetwarzania klauzule jest:</span><span class="sxs-lookup"><span data-stu-id="650b0-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="650b0-125">Klauzula FROM</span><span class="sxs-lookup"><span data-stu-id="650b0-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="650b0-126">Klauzula WHERE</span><span class="sxs-lookup"><span data-stu-id="650b0-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="650b0-127">Klauzula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="650b0-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="650b0-128">Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="650b0-129">Należy pamiętać, że jest inna niż kolejność hello, w jakiej występują w składni hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="650b0-130">porządkowanie Hello jest taka, że wszystkie nowe symbole wynikające z klauzulą przetworzonych są widoczne i mogą być używane w klauzulach później przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="650b0-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="650b0-131">Na przykład w przypadku gdy aliasów zadeklarować w klauzuli FROM są dostępne i klauzule SELECT.</span><span class="sxs-lookup"><span data-stu-id="650b0-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="650b0-132">**Odstęp i komentarze**</span><span class="sxs-lookup"><span data-stu-id="650b0-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="650b0-133">Wszystkie białe znaki, które nie są częścią ciągu w cudzysłowie lub identyfikator w cudzysłowach nie są częścią gramatyki języka hello i są ignorowane podczas analizy.</span><span class="sxs-lookup"><span data-stu-id="650b0-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="650b0-134">język zapytań Hello obsługuje komentarzy styl T-SQL, takich jak</span><span class="sxs-lookup"><span data-stu-id="650b0-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="650b0-135">Instrukcja SQL`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="650b0-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="650b0-136">Gdy znaków odstępu i komentarze nie ma żadnego znaczenia w gramatyce hello, muszą być używane tooseparate tokenów.</span><span class="sxs-lookup"><span data-stu-id="650b0-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="650b0-137">Na przykład: `-1e5` jest chwilę jednego tokenu, liczba`: – 1 e5` minus token następuje numer 1 i identyfikatora e5.</span><span class="sxs-lookup"><span data-stu-id="650b0-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="650b0-138"><a name="bk_select_query"></a>Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="650b0-139">klauzule Hello w instrukcji SELECT hello muszą być uporządkowane, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="650b0-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="650b0-140">Jeden z hello opcjonalna klauzula można pominąć.</span><span class="sxs-lookup"><span data-stu-id="650b0-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="650b0-141">Jednak w przypadku używania klauzule opcjonalne muszą występować w odpowiedniej kolejności hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="650b0-142">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="650b0-143">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="650b0-144">Ustaw właściwości lub wartości toobe wybrane dla wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="650b0-145">Określa, że wartość hello powinny zostać pobrane bez wprowadzania żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="650b0-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="650b0-146">W szczególności, jeśli wartość hello przetwarzane jest obiektem, będzie można pobrać wszystkich właściwości.</span><span class="sxs-lookup"><span data-stu-id="650b0-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="650b0-147">Określa listę hello toobe właściwości pobrać.</span><span class="sxs-lookup"><span data-stu-id="650b0-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="650b0-148">Wartości zwracane będzie obiekt o właściwości hello określone.</span><span class="sxs-lookup"><span data-stu-id="650b0-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="650b0-149">Określa, że wartość JSON hello powinny zostać pobrane zamiast hello cały obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="650b0-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="650b0-150">To, w przeciwieństwie do `<property_list>` nie jest zawijany hello prognozowane wartości w obiekcie.</span><span class="sxs-lookup"><span data-stu-id="650b0-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="650b0-151">Wyrażenie odpowiadające hello toobe wartość obliczana.</span><span class="sxs-lookup"><span data-stu-id="650b0-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="650b0-152">Zobacz [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="650b0-153">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-153">**Remarks**</span></span>  
  
<span data-ttu-id="650b0-154">Witaj `SELECT *` składnia jest prawidłowa, jeśli klauzula FROM została zadeklarowana dokładnie jeden alias.</span><span class="sxs-lookup"><span data-stu-id="650b0-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="650b0-155">`SELECT *`udostępnia projekcji tożsamości, które mogą być przydatne, jeśli nie projekcji nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="650b0-156">Wybierz * jest prawidłowa, jeśli klauzula FROM określono i wprowadzono tylko jednego źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="650b0-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="650b0-157">Należy pamiętać, że `SELECT <select_list>` i `SELECT *` są "sugar składni" i może być również wyrażona za pomocą prostego instrukcji "SELECT", jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="650b0-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="650b0-158">odpowiada to:</span><span class="sxs-lookup"><span data-stu-id="650b0-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="650b0-159">odpowiada to:</span><span class="sxs-lookup"><span data-stu-id="650b0-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="650b0-160">**Zobacz też**</span><span class="sxs-lookup"><span data-stu-id="650b0-160">**See Also**</span></span>  
  
[<span data-ttu-id="650b0-161">Wyrażenia skalarne</span><span class="sxs-lookup"><span data-stu-id="650b0-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="650b0-162">Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="650b0-163"><a name="bk_from_clause"></a>Klauzula FROM</span><span class="sxs-lookup"><span data-stu-id="650b0-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="650b0-164">Określa źródło hello lub dołączonym do źródła.</span><span class="sxs-lookup"><span data-stu-id="650b0-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="650b0-165">Klauzula FROM Hello jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="650b0-165">hello FROM clause is optional.</span></span> <span data-ttu-id="650b0-166">Jeśli nie jest określony, inne klauzule nadal będą wykonywane tak, jakby klauzuli FROM podane pojedynczego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="650b0-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="650b0-167">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="650b0-168">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="650b0-169">Określa źródło danych, z lub bez aliasu.</span><span class="sxs-lookup"><span data-stu-id="650b0-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="650b0-170">Jeśli nie określono aliasu, będzie można wywnioskować na podstawie hello `<collection_expression>` za pomocą następujących reguł:</span><span class="sxs-lookup"><span data-stu-id="650b0-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="650b0-171">Jeśli wyrażenie hello jest nazwa_kolekcji, nazwa_kolekcji będzie używany jako alias.</span><span class="sxs-lookup"><span data-stu-id="650b0-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="650b0-172">Jeśli wyrażenie hello jest `<collection_expression>`, property_name, a następnie property_name zostanie użyta jako alias.</span><span class="sxs-lookup"><span data-stu-id="650b0-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="650b0-173">Jeśli wyrażenie hello jest nazwa_kolekcji, nazwa_kolekcji będzie używany jako alias.</span><span class="sxs-lookup"><span data-stu-id="650b0-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="650b0-174">JAKO`input_alias`</span><span class="sxs-lookup"><span data-stu-id="650b0-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="650b0-175">Określa, że hello `input_alias` to zbiór wartości zwracanych przez hello bazowy wyrażeniu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="650b0-176">`input_alias`W</span><span class="sxs-lookup"><span data-stu-id="650b0-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="650b0-177">Określa, że hello `input_alias` powinno reprezentować hello zbiór wartości uzyskane przez Iterowanie po każdej tablica zwrócona przez hello bazowy wyrażeniu kolekcji wszystkie elementy tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="650b0-178">Każda wartość zwracana przez podstawowej wyrażeniu kolekcji, która nie jest tablicą jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="650b0-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="650b0-179">Określa, że hello kolekcji wyrażenie toobe używanych tooretrieve hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="650b0-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="650b0-180">Określa, że w tym dokumencie powinny zostać pobrane z hello domyślnie kolekcji aktualnie połączonych.</span><span class="sxs-lookup"><span data-stu-id="650b0-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="650b0-181">Określa, że tego dokumentu powinny zostać pobrane z kolekcji hello podane.</span><span class="sxs-lookup"><span data-stu-id="650b0-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="650b0-182">Nazwa Hello kolekcji hello musi odpowiadać nazwie hello kolekcji hello aktualnie połączony.</span><span class="sxs-lookup"><span data-stu-id="650b0-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="650b0-183">Określa, w tym dokumencie powinny zostać pobrane z hello innego źródła, zdefiniowany przez hello podany alias.</span><span class="sxs-lookup"><span data-stu-id="650b0-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="650b0-184">Określa, w tym dokumencie powinny zostać pobrane po zalogowaniu się do hello `property_name` właściwości lub indeks_tablicy elementu tablicy dla wszystkich dokumentów pobierane przez określone wyrażenie kolekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="650b0-185">Określa, w tym dokumencie powinny zostać pobrane po zalogowaniu się do hello `property_name` właściwości lub indeks_tablicy elementu tablicy dla wszystkich dokumentów pobierane przez określone wyrażenie kolekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="650b0-186">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-186">**Remarks**</span></span>  
  
<span data-ttu-id="650b0-187">Wszystkie aliasy dostarczona lub wywnioskować w hello `<from_source>(`s) musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="650b0-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="650b0-188">Witaj składni `<collection_expression>.`property_name jest identyczny hello `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="650b0-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="650b0-189">Jednak hello później można używać składni Jeśli nazwa właściwości zawiera znaki innego niż identyfikator.</span><span class="sxs-lookup"><span data-stu-id="650b0-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="650b0-190">**Brak elementów tablicy nie ma właściwości niezdefiniowanych wartości obsługi**</span><span class="sxs-lookup"><span data-stu-id="650b0-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="650b0-191">Wyrażeniu kolekcji uzyskuje dostęp do właściwości lub elementów tablicy i że nie ma wartości, tej wartości będą ignorowane i nie można przetworzyć więcej.</span><span class="sxs-lookup"><span data-stu-id="650b0-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="650b0-192">**Kolekcja wyrażeń kontekstu zakresu**</span><span class="sxs-lookup"><span data-stu-id="650b0-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="650b0-193">Wyrażeniu kolekcji może być zakresem kolekcji lub zakres dokumentu:</span><span class="sxs-lookup"><span data-stu-id="650b0-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="650b0-194">Wyrażenie jest zakres kolekcji, jeśli hello źródła wyrażeniu kolekcji hello jest albo głównego lub `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="650b0-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="650b0-195">Takie wyrażenie reprezentuje zestaw dokumentów pobierane z kolekcji hello bezpośrednio i nie jest zależna od przetwarzania hello innych wyrażeń kolekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="650b0-196">Wyrażenie jest zakres dokumentu, jeśli hello źródła wyrażeniu kolekcji hello jest `input_alias` wprowadzone we wcześniejszej części hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="650b0-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="650b0-197">Takie wyrażenie reprezentuje zestaw dokumentów uzyskany przez obliczenie hello wyrażeniu kolekcji w zakresie hello każdego dokumentu należących zestaw toohello skojarzony z kolekcją aliasem hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="650b0-198">Wynikowy zestaw Hello będzie Unii zestawów uzyskany przez obliczenie hello kolekcji wyrażenia dla każdego z dokumentów hello w hello podstawowy zestaw.</span><span class="sxs-lookup"><span data-stu-id="650b0-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="650b0-199">**Tworzy sprzężenie**</span><span class="sxs-lookup"><span data-stu-id="650b0-199">**Joins**</span></span>  
  
<span data-ttu-id="650b0-200">W bieżącej wersji hello Azure DB rozwiązania Cosmos obsługuje sprzężeń wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="650b0-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="650b0-201">Nadchodzącego są sprzężenia dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="650b0-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="650b0-202">Wynik sprzężenia wewnętrzne w pełny iloczyn wektorowy hello ustawia uczestniczących hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="650b0-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="650b0-203">wynik Hello N sposób sprzężenia jest zestaw spójnych kolekcji z elementu N, gdzie każdej wartości w krotce hello jest skojarzony z aliasem hello ustawić uczestniczących hello sprzężenia i jest możliwy za pomocą odwołań do tego aliasu w innych klauzul.</span><span class="sxs-lookup"><span data-stu-id="650b0-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="650b0-204">oceny Hello sprzężenia hello zależy od zakresu kontekstu hello hello uczestniczących zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="650b0-205">Sprzężenia między kolekcji zestawu A i zakres kolekcji ustawić B, wynikiem iloczyn wektorowy wszystkie elementy w zestawach A i B.</span><span class="sxs-lookup"><span data-stu-id="650b0-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="650b0-206">Powoduje sprzężenie zestaw A i zestaw zakres dokumentu B, w związku z wszystkich zestawów uzyskany przez obliczenie zakres dokumentu zestawu B dla każdego dokumentu z ustawić A.</span><span class="sxs-lookup"><span data-stu-id="650b0-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="650b0-207">W bieżącej wersji hello maksymalnie jedno wyrażenie zakres kolekcji jest obsługiwany przez procesor zapytań hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="650b0-208">**Przykłady sprzężeń:**</span><span class="sxs-lookup"><span data-stu-id="650b0-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="650b0-209">Przyjrzyjmy się powitania po klauzuli FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="650b0-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="650b0-210">Let każdego źródła Zdefiniuj `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="650b0-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="650b0-211">Tej klauzuli FROM zwraca zestaw spójnych kolekcji na N (krotka z wartościami N).</span><span class="sxs-lookup"><span data-stu-id="650b0-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="650b0-212">Każda krotka zawiera wartości utworzonego przez Iterowanie wszystkie aliasy kolekcji po ich odpowiednich zestawów.</span><span class="sxs-lookup"><span data-stu-id="650b0-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="650b0-213">*Dołącz do SPOŁECZNOŚCI przykład 1 z 2 źródeł:*</span><span class="sxs-lookup"><span data-stu-id="650b0-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="650b0-214">Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="650b0-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="650b0-215">Let `<from_source2>` można dokumentu o zakresie odwołujące się do input_alias1 i reprezentują zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="650b0-216">{1, 2} dla`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="650b0-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="650b0-217">{3} dla`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="650b0-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="650b0-218">{4, 5} dla`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="650b0-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="650b0-219">Witaj w klauzuli FROM `<from_source1> JOIN <from_source2>` spowoduje następujące krotek hello:</span><span class="sxs-lookup"><span data-stu-id="650b0-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="650b0-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="650b0-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="650b0-221">*Dołącz do SPOŁECZNOŚCI przykład 2 z 3 źródeł:*</span><span class="sxs-lookup"><span data-stu-id="650b0-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="650b0-222">Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="650b0-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="650b0-223">Let `<from_source2>` się zakres dokument odwołuje się do `input_alias1` i reprezentują zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="650b0-224">{1, 2} dla`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="650b0-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="650b0-225">{3} dla`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="650b0-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="650b0-226">{4, 5} dla`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="650b0-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="650b0-227">Let `<from_source3>` się zakres dokument odwołuje się do `input_alias2` i reprezentują zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="650b0-228">{100, 200} dla`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="650b0-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="650b0-229">{300} dla`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="650b0-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="650b0-230">Witaj w klauzuli FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` spowoduje następujące krotek hello:</span><span class="sxs-lookup"><span data-stu-id="650b0-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="650b0-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="650b0-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="650b0-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="650b0-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="650b0-233">Brak spójnych kolekcji dla innych wartości `input_alias1`, `input_alias2`, dla których hello `<from_source3>` nie zwrócił żadnych wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="650b0-234">*Dołącz do SPOŁECZNOŚCI przykład 3 z 3 źródeł:*</span><span class="sxs-lookup"><span data-stu-id="650b0-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="650b0-235">Let < from_source1 > można zakres kolekcji i reprezentują zestaw {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="650b0-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="650b0-236">Let `<from_source1>` się o zakresie kolekcji i reprezentują zestaw {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="650b0-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="650b0-237">Pozwól < from_source2 > można input_alias1 odwołującego się o zakresie dokumentu i reprezentują zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="650b0-238">{1, 2} dla`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="650b0-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="650b0-239">{3} dla`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="650b0-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="650b0-240">{4, 5} dla`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="650b0-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="650b0-241">Let `<from_source3>` wchodzą do zakresu zbyt`input_alias1` i reprezentują zestawów:</span><span class="sxs-lookup"><span data-stu-id="650b0-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="650b0-242">{100, 200} dla`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="650b0-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="650b0-243">{300} dla`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="650b0-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="650b0-244">Witaj w klauzuli FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` spowoduje następujące krotek hello:</span><span class="sxs-lookup"><span data-stu-id="650b0-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="650b0-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="650b0-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="650b0-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), C, 4, 300, (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="650b0-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="650b0-247">Spowodowało to iloczyn wektorowy między `<from_source2>` i `<from_source3>` ponieważ oba są zakresami toohello tego samego `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="650b0-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="650b0-248">Spowodowało to 4 (2 x 2) spójnych kolekcji o wartości A, 0 spójnych kolekcji o wartości B (1 x 0) i 2 (2 x 1) spójnych kolekcji o wartości C.</span><span class="sxs-lookup"><span data-stu-id="650b0-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="650b0-249">**Zobacz też**</span><span class="sxs-lookup"><span data-stu-id="650b0-249">**See also**</span></span>  
  
 [<span data-ttu-id="650b0-250">Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="650b0-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="650b0-251"><a name="bk_where_clause"></a>Klauzula WHERE</span><span class="sxs-lookup"><span data-stu-id="650b0-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="650b0-252">Określa warunek wyszukiwania hello dokumentów hello zwróconych przez zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="650b0-253">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="650b0-254">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="650b0-255">Określa toobe warunku hello spełnia hello toobe dokumenty zwrócone.</span><span class="sxs-lookup"><span data-stu-id="650b0-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="650b0-256">Wyrażenie odpowiadające hello toobe wartość obliczana.</span><span class="sxs-lookup"><span data-stu-id="650b0-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="650b0-257">Zobacz hello [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="650b0-258">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-258">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-259">Aby hello toobe dokumentu zwracane wyrażenie określone jako warunek filtru musi zwrócić tootrue.</span><span class="sxs-lookup"><span data-stu-id="650b0-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="650b0-260">Tylko wartość logiczną PRAWDA będzie spełniają warunek hello, wszelkie inne wartości: niezdefiniowana, null, wartość false, numer, tablicy lub obiekt nie spełniają warunek hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="650b0-261"><a name="bk_orderby_clause"></a>Klauzula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="650b0-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="650b0-262">Określa sortowanie kolejność wyników zwróconych przez zapytanie hello hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="650b0-263">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="650b0-264">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="650b0-265">Określa właściwość lub wyrażenie, na którym zestawu wyników kwerendy hello toosort.</span><span class="sxs-lookup"><span data-stu-id="650b0-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="650b0-266">Sortuj kolumny można określić jako alias nazwy lub kolumny.</span><span class="sxs-lookup"><span data-stu-id="650b0-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="650b0-267">Można określić wiele kolumn sortowania.</span><span class="sxs-lookup"><span data-stu-id="650b0-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="650b0-268">Nazwy kolumn muszą być unikatowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-268">Column names must be unique.</span></span> <span data-ttu-id="650b0-269">Sekwencja Hello hello sortowania kolumn w klauzuli ORDER BY hello definiuje hello organizacji hello sortowane zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="650b0-270">To, że zestaw wyników hello są sortowane według hello pierwszą właściwością i następnie tej listy uporządkowanej są sortowane według właściwości drugi hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="650b0-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="650b0-271">Witaj nazwy kolumn w klauzuli ORDER BY hello musi odpowiadać tooeither kolumny w hello wybierz kolumny z listy lub tooa zdefiniowany w tabeli określonej w klauzuli FROM hello bez żadnych niejednoznaczności.</span><span class="sxs-lookup"><span data-stu-id="650b0-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="650b0-272">Określa jedną właściwość lub wyrażenie, na które zestawu wyników zapytania hello toosort.</span><span class="sxs-lookup"><span data-stu-id="650b0-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="650b0-273">Zobacz hello [wyrażenia skalarne](#bk_scalar_expressions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="650b0-274">Określa, że hello wartości w określonej kolumnie hello mają być sortowane w kolejności rosnącej lub malejącej.</span><span class="sxs-lookup"><span data-stu-id="650b0-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="650b0-275">Sortuje ASC od wartości toohighest hello najniższej wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="650b0-276">Sortuje DESC z najwyższą wartością toolowest wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="650b0-277">ASC jest hello domyślny porządek sortowania.</span><span class="sxs-lookup"><span data-stu-id="650b0-277">ASC is hello default sort order.</span></span> <span data-ttu-id="650b0-278">Wartości null są traktowane jako hello najmniejsze możliwe wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="650b0-279">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-279">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-280">Podczas hello gramatyki zapytań obsługuje wiele kolejność według właściwości, czasu wykonywania zapytania bazy danych Azure rozwiązania Cosmos hello obsługuje sortowanie, tylko jednej właściwości oraz tylko z nazwy właściwości, tj., nie dla właściwości obliczanej.</span><span class="sxs-lookup"><span data-stu-id="650b0-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="650b0-281">Sortowanie wymaga również tego hello indeksowania zasad zawiera indeks zakresu dla właściwości hello i hello określony typ, z hello maksymalna dokładność.</span><span class="sxs-lookup"><span data-stu-id="650b0-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="650b0-282">Zobacz toohello indeksowania dokumentacji zasad, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="650b0-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="650b0-283"><a name="bk_scalar_expressions"></a>Wyrażenia skalarne</span><span class="sxs-lookup"><span data-stu-id="650b0-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="650b0-284">Wyrażenie skalarne jest kombinacją symboli i operatory, które mogą być ocenione tooobtain pojedynczą wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="650b0-285">Proste wyrażenia mogą być stałe, odwołań do właściwości, odwołania do elementu tablicy, odwołania do aliasu lub wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="650b0-286">Proste wyrażenia można łączyć przy użyciu operatorów wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="650b0-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="650b0-287">Aby uzyskać szczegółowe informacje, na których wyrażenie skalarne może mieć wartości, zobacz [stałe](#bk_constants) sekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="650b0-288">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="650b0-289">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="650b0-290">Reprezentuje wartość stałą.</span><span class="sxs-lookup"><span data-stu-id="650b0-290">Represents a constant value.</span></span> <span data-ttu-id="650b0-291">Zobacz [stałe](#bk_constants) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="650b0-292">Reprezentuje wartość zdefiniowana przez hello `input_alias` wprowadzone w hello `FROM` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="650b0-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="650b0-293">Ta wartość jest gwarantowana toonot można **Niezdefiniowany** —**Niezdefiniowany** wartości w danych wejściowych hello są pomijane.</span><span class="sxs-lookup"><span data-stu-id="650b0-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="650b0-294">Reprezentuje wartość hello właściwości obiektu.</span><span class="sxs-lookup"><span data-stu-id="650b0-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="650b0-295">Jeśli właściwość hello nie istnieje lub odwołuje się do właściwości na wartość, która nie jest obiektem, a następnie hello wyrażenie zbyt**Niezdefiniowany** wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="650b0-296">Reprezentuje wartość hello właściwość o nazwie `property_name` lub element tablicy o indeksie `array_index` obiektu/tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="650b0-297">Jeśli indeks tablicy właściwości/hello nie istnieje lub indeks tablicy właściwości/hello odwołuje się do wartości, która nie jest Tablica obiektów /, następnie hello wynikiem wyrażenia jest wartość tooundefined.</span><span class="sxs-lookup"><span data-stu-id="650b0-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="650b0-298">Reprezentuje operator, który jest stosowane tooa pojedyncza wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="650b0-299">Zobacz [operatory](#bk_operators) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="650b0-300">Reprezentuje operatora, który jest stosowane tootwo wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="650b0-301">Zobacz [operatory](#bk_operators) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="650b0-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="650b0-302">Reprezentuje wartość zdefiniowana przez wynik wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="650b0-303">Nazwa użytkownika, powitalne zdefiniowane skalarną.</span><span class="sxs-lookup"><span data-stu-id="650b0-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="650b0-304">Nazwa wbudowanej funkcji skalarnych hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="650b0-305">Reprezentuje wartość uzyskany przez utworzenie nowego obiektu o określonej właściwości i ich wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="650b0-306">Reprezentuje wartość uzyskany przez utworzenie nowej tablicy z określonymi wartościami jako elementy</span><span class="sxs-lookup"><span data-stu-id="650b0-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="650b0-307">Reprezentuje wartość hello określona nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="650b0-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="650b0-308">Nazwy parametrów muszą mieć pojedynczy @ jako pierwszy znak hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="650b0-309">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-309">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-310">Podczas wywoływania wbudowanych lub użytkownika definiowania funkcji skalarnych muszą być zdefiniowane wszystkie argumenty.</span><span class="sxs-lookup"><span data-stu-id="650b0-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="650b0-311">Jeśli dowolny z argumentów hello jest niezdefiniowana, nie zostanie wywołana funkcja hello i hello wynik będzie niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="650b0-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="650b0-312">Podczas tworzenia obiektu, dowolnej właściwości, która jest przypisana niezdefiniowana wartość zostanie pominięty i nie jest uwzględniony w hello utworzony obiekt.</span><span class="sxs-lookup"><span data-stu-id="650b0-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="650b0-313">Podczas tworzenia tablicy wartości elementu, który jest przypisany **Niezdefiniowany** wartość zostanie pominięty i nie jest uwzględniony w obiekcie hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="650b0-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="650b0-314">Hello obok zdefiniowany element tootake spowoduje jego miejsce w taki sposób, że tablica hello utworzone zostanie nie zostały pominięte indeksów.</span><span class="sxs-lookup"><span data-stu-id="650b0-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="650b0-315"><a name="bk_operators"></a>Operatory</span><span class="sxs-lookup"><span data-stu-id="650b0-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="650b0-316">W tej sekcji opisano operatory hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="650b0-316">This section describes hello supported operators.</span></span> <span data-ttu-id="650b0-317">Każdy operator może być przypisany tooexactly jedną kategorię.</span><span class="sxs-lookup"><span data-stu-id="650b0-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="650b0-318">Zobacz **kategorii Operator** tabelę poniżej, aby uzyskać szczegółowe informacje dotyczące obsługi **Niezdefiniowany** wartości typu wymagania dotyczące obsługi z niezgodne typy wartości i wartości wejściowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="650b0-319">**Operator kategorie:**</span><span class="sxs-lookup"><span data-stu-id="650b0-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="650b0-320">**Kategoria**</span><span class="sxs-lookup"><span data-stu-id="650b0-320">**Category**</span></span>|<span data-ttu-id="650b0-321">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="650b0-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="650b0-322">**operacje arytmetyczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-322">**arithmetic**</span></span>|<span data-ttu-id="650b0-323">Operator oczekuje input(s) toobe numery.</span><span class="sxs-lookup"><span data-stu-id="650b0-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="650b0-324">Dane wyjściowe również jest liczbą.</span><span class="sxs-lookup"><span data-stu-id="650b0-324">Output is also a Number.</span></span> <span data-ttu-id="650b0-325">Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub jest typu innego niż wynik numer, a następnie hello **Niezdefiniowany**.</span><span class="sxs-lookup"><span data-stu-id="650b0-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="650b0-326">**bitowe**</span><span class="sxs-lookup"><span data-stu-id="650b0-326">**bitwise**</span></span>|<span data-ttu-id="650b0-327">Operator oczekuje input(s) toobe 32-bitowej liczby całkowitej ze znakiem numery.</span><span class="sxs-lookup"><span data-stu-id="650b0-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="650b0-328">Dane wyjściowe jest również 32-bitowa liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="650b0-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="650b0-329">Zostanie zaokrąglony żadnej wartości niebędące liczbami całkowitymi.</span><span class="sxs-lookup"><span data-stu-id="650b0-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="650b0-330">Wartość dodatnią zostaną zaokrąglone w dół, ujemne wartości zaokrąglona w górę.</span><span class="sxs-lookup"><span data-stu-id="650b0-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="650b0-331">Każdą wartość, która znajduje się poza zakresem 32-bitową liczbę całkowitą hello zostanie przekonwertowany, wykonując ostatnich 32 bity jego dwa w notacji uzupełnienia.</span><span class="sxs-lookup"><span data-stu-id="650b0-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="650b0-332">Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub wpisz inne niż numer, a następnie wynik hello jest **Niezdefiniowany**.</span><span class="sxs-lookup"><span data-stu-id="650b0-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="650b0-333">**Uwaga:** hello powyżej zachowanie jest zgodne z zachowanie bitowy operator w JavaScript.</span><span class="sxs-lookup"><span data-stu-id="650b0-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="650b0-334">**logiczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-334">**logical**</span></span>|<span data-ttu-id="650b0-335">Operator oczekuje input(s) toobe Boolean(s).</span><span class="sxs-lookup"><span data-stu-id="650b0-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="650b0-336">Dane wyjściowe również jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="650b0-337">Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub typu, innego niż Boolean, hello wynikiem będzie **Niezdefiniowany**.</span><span class="sxs-lookup"><span data-stu-id="650b0-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="650b0-338">**Porównanie**</span><span class="sxs-lookup"><span data-stu-id="650b0-338">**comparison**</span></span>|<span data-ttu-id="650b0-339">Operator oczekuje input(s) hello toohave sam typu i nie jest niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="650b0-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="650b0-340">Dane wyjściowe jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="650b0-341">Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub hello dane wejściowe mają różne typy, a następnie wynik hello jest **Niezdefiniowany**.</span><span class="sxs-lookup"><span data-stu-id="650b0-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="650b0-342">Zobacz **porządkowanie wartości do porównania** tabeli dla wartości kolejności szczegóły.</span><span class="sxs-lookup"><span data-stu-id="650b0-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="650b0-343">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="650b0-343">**string**</span></span>|<span data-ttu-id="650b0-344">Operator oczekuje input(s) toobe ciągi.</span><span class="sxs-lookup"><span data-stu-id="650b0-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="650b0-345">Dane wyjściowe również jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="650b0-345">Output is also a String.</span></span><br /><span data-ttu-id="650b0-346">Jeśli dowolny z wejść hello jest **Niezdefiniowany** lub jest typu innego niż wynik ciągu, a następnie hello **Niezdefiniowany**.</span><span class="sxs-lookup"><span data-stu-id="650b0-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="650b0-347">**Operatory jednoargumentowe:**</span><span class="sxs-lookup"><span data-stu-id="650b0-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="650b0-348">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="650b0-348">**Name**</span></span>|<span data-ttu-id="650b0-349">**Operator**</span><span class="sxs-lookup"><span data-stu-id="650b0-349">**Operator**</span></span>|<span data-ttu-id="650b0-350">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="650b0-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="650b0-351">**operacje arytmetyczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="650b0-352">Zwraca wartość liczbową hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="650b0-353">Bitową negację.</span><span class="sxs-lookup"><span data-stu-id="650b0-353">Bitwise negation.</span></span> <span data-ttu-id="650b0-354">Zwraca zanegowane wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="650b0-355">**bitowe**</span><span class="sxs-lookup"><span data-stu-id="650b0-355">**bitwise**</span></span>|~|<span data-ttu-id="650b0-356">Uzupełnienie tych.</span><span class="sxs-lookup"><span data-stu-id="650b0-356">Ones' complement.</span></span> <span data-ttu-id="650b0-357">Zwraca uzupełnienie wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="650b0-358">**Logiczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-358">**Logical**</span></span>|<span data-ttu-id="650b0-359">**NIE**</span><span class="sxs-lookup"><span data-stu-id="650b0-359">**NOT**</span></span>|<span data-ttu-id="650b0-360">Negacja.</span><span class="sxs-lookup"><span data-stu-id="650b0-360">Negation.</span></span> <span data-ttu-id="650b0-361">Zwraca zanegowane wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="650b0-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="650b0-362">**Operatory binarne:**</span><span class="sxs-lookup"><span data-stu-id="650b0-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="650b0-363">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="650b0-363">**Name**</span></span>|<span data-ttu-id="650b0-364">**Operator**</span><span class="sxs-lookup"><span data-stu-id="650b0-364">**Operator**</span></span>|<span data-ttu-id="650b0-365">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="650b0-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="650b0-366">**operacje arytmetyczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="650b0-367">Dodatek.</span><span class="sxs-lookup"><span data-stu-id="650b0-367">Addition.</span></span><br /><br /> <span data-ttu-id="650b0-368">Odejmowanie.</span><span class="sxs-lookup"><span data-stu-id="650b0-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="650b0-369">Mnożenia.</span><span class="sxs-lookup"><span data-stu-id="650b0-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="650b0-370">Podział.</span><span class="sxs-lookup"><span data-stu-id="650b0-370">Division.</span></span><br /><br /> <span data-ttu-id="650b0-371">Modulacji.</span><span class="sxs-lookup"><span data-stu-id="650b0-371">Modulation.</span></span>|  
|<span data-ttu-id="650b0-372">**bitowe**</span><span class="sxs-lookup"><span data-stu-id="650b0-372">**bitwise**</span></span>|<span data-ttu-id="650b0-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="650b0-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="650b0-374">Wartość logiczną lub.</span><span class="sxs-lookup"><span data-stu-id="650b0-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="650b0-375">Bitowe koniunkcji binarnej.</span><span class="sxs-lookup"><span data-stu-id="650b0-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="650b0-376">Iloczynu bitowego XOR.</span><span class="sxs-lookup"><span data-stu-id="650b0-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="650b0-377">Przesunięcia w lewo.</span><span class="sxs-lookup"><span data-stu-id="650b0-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="650b0-378">Przesunięcia w prawo.</span><span class="sxs-lookup"><span data-stu-id="650b0-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="650b0-379">Przesunięcia w prawo wypełnienia zero.</span><span class="sxs-lookup"><span data-stu-id="650b0-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="650b0-380">**logiczne**</span><span class="sxs-lookup"><span data-stu-id="650b0-380">**logical**</span></span>|<span data-ttu-id="650b0-381">**I**</span><span class="sxs-lookup"><span data-stu-id="650b0-381">**AND**</span></span><br /><br /> <span data-ttu-id="650b0-382">**LUB**</span><span class="sxs-lookup"><span data-stu-id="650b0-382">**OR**</span></span>|<span data-ttu-id="650b0-383">Połączenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-383">Logical conjunction.</span></span> <span data-ttu-id="650b0-384">Zwraca **true** Jeśli oba argumenty mają **true**, zwraca **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-385">Połączenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-385">Logical conjunction.</span></span> <span data-ttu-id="650b0-386">Zwraca **true** Jeśli oba argumenty mają **true**, zwraca **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="650b0-387">**Porównanie**</span><span class="sxs-lookup"><span data-stu-id="650b0-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="650b0-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="650b0-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="650b0-389">**??**</span><span class="sxs-lookup"><span data-stu-id="650b0-389">**??**</span></span>|<span data-ttu-id="650b0-390">Równa się.</span><span class="sxs-lookup"><span data-stu-id="650b0-390">Equals.</span></span> <span data-ttu-id="650b0-391">Zwraca **true** argumenty są takie same, funkcja zwraca **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-392">Nie równa się.</span><span class="sxs-lookup"><span data-stu-id="650b0-392">Not equal to.</span></span> <span data-ttu-id="650b0-393">Zwraca **true** argumenty nie są równe, zwraca **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-394">Większa.</span><span class="sxs-lookup"><span data-stu-id="650b0-394">Greater Than.</span></span> <span data-ttu-id="650b0-395">Zwraca **true** Jeśli pierwszy argument jest większy niż drugi hello, **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-396">Większe lub równe.</span><span class="sxs-lookup"><span data-stu-id="650b0-396">Greater Than or Equal To.</span></span> <span data-ttu-id="650b0-397">Zwraca **true** Jeśli pierwszy argument jest większa niż lub równa toohello drugi z nich, zwróć **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-398">Poniżej.</span><span class="sxs-lookup"><span data-stu-id="650b0-398">Less Than.</span></span> <span data-ttu-id="650b0-399">Zwraca **true** Jeśli pierwszy argument jest mniejszy niż drugi Witaj, zwróć **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-400">Mniejsze niż lub równe.</span><span class="sxs-lookup"><span data-stu-id="650b0-400">Less Than or Equal To.</span></span> <span data-ttu-id="650b0-401">Zwraca **true** Jeśli pierwszy argument jest mniejsza lub równa toohello drugie jedną zwracany **false** inaczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="650b0-402">Połączenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-402">Coalesce.</span></span> <span data-ttu-id="650b0-403">Zwraca hello drugi argument, jeśli pierwszy argument hello jest **Niezdefiniowany** wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="650b0-404">**Ciąg**</span><span class="sxs-lookup"><span data-stu-id="650b0-404">**String**</span></span>|<span data-ttu-id="650b0-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="650b0-405">**&#124;&#124;**</span></span>|<span data-ttu-id="650b0-406">Łączenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-406">Concatenation.</span></span> <span data-ttu-id="650b0-407">Zwraca złączeniem oba argumenty.</span><span class="sxs-lookup"><span data-stu-id="650b0-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="650b0-408">**Operatory trzyargumentowe:**</span><span class="sxs-lookup"><span data-stu-id="650b0-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="650b0-409">Operator trójargumentowy</span><span class="sxs-lookup"><span data-stu-id="650b0-409">Ternary operator</span></span>|<span data-ttu-id="650b0-410">?</span><span class="sxs-lookup"><span data-stu-id="650b0-410">?</span></span>|<span data-ttu-id="650b0-411">Zwraca hello drugi argument, jeśli pierwszy argument hello zbyt**true**; w przeciwnym razie zwraca hello trzeci argument.</span><span class="sxs-lookup"><span data-stu-id="650b0-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="650b0-412">**Kolejność wartości do porównania**</span><span class="sxs-lookup"><span data-stu-id="650b0-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="650b0-413">**Typ**</span><span class="sxs-lookup"><span data-stu-id="650b0-413">**Type**</span></span>|<span data-ttu-id="650b0-414">**Kolejność wartości**</span><span class="sxs-lookup"><span data-stu-id="650b0-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="650b0-415">**Niezdefiniowana**</span><span class="sxs-lookup"><span data-stu-id="650b0-415">**Undefined**</span></span>|<span data-ttu-id="650b0-416">Nie można porównywać.</span><span class="sxs-lookup"><span data-stu-id="650b0-416">Not comparable.</span></span>|  
|<span data-ttu-id="650b0-417">**Wartość null**</span><span class="sxs-lookup"><span data-stu-id="650b0-417">**Null**</span></span>|<span data-ttu-id="650b0-418">Pojedyncza wartość: **wartości null**</span><span class="sxs-lookup"><span data-stu-id="650b0-418">Single value: **null**</span></span>|  
|<span data-ttu-id="650b0-419">**Numer**</span><span class="sxs-lookup"><span data-stu-id="650b0-419">**Number**</span></span>|<span data-ttu-id="650b0-420">Liczba rzeczywista fizycznych.</span><span class="sxs-lookup"><span data-stu-id="650b0-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="650b0-421">Wartości nieskończoności ujemnej jest mniejszy niż inne wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="650b0-422">Dodatnia wartość Infinity jest większy niż inne wartość liczbową. **NaN** wartość nie jest on porównywalny.</span><span class="sxs-lookup"><span data-stu-id="650b0-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="650b0-423">Porównanie z **NaN** spowoduje **Niezdefiniowany** wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="650b0-424">**Ciąg**</span><span class="sxs-lookup"><span data-stu-id="650b0-424">**String**</span></span>|<span data-ttu-id="650b0-425">Kolejność lexicographical.</span><span class="sxs-lookup"><span data-stu-id="650b0-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="650b0-426">**Tablica**</span><span class="sxs-lookup"><span data-stu-id="650b0-426">**Array**</span></span>|<span data-ttu-id="650b0-427">Nie określania kolejności, ale słuszne.</span><span class="sxs-lookup"><span data-stu-id="650b0-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="650b0-428">**Obiekt**</span><span class="sxs-lookup"><span data-stu-id="650b0-428">**Object**</span></span>|<span data-ttu-id="650b0-429">Nie określania kolejności, ale słuszne.</span><span class="sxs-lookup"><span data-stu-id="650b0-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="650b0-430">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-430">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-431">W usłudze Azure DB rozwiązania Cosmos hello typy wartości, często nie są znane, do momentu rzeczywistości pobrania z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="650b0-432">Kolejność toosupport wydajność wykonywania zapytań większość operatorów hello ma wymagania typu strict.</span><span class="sxs-lookup"><span data-stu-id="650b0-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="650b0-433">Operatory samodzielnie nie wykonuj również niejawną konwersję.</span><span class="sxs-lookup"><span data-stu-id="650b0-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="650b0-434">Oznacza to, że zapytanie, takich jak: Wybierz * z katalogu głównego r WHERE r.Age = 21 zwróci tylko te dokumenty z właściwością liczby równy toohello wieku 21.</span><span class="sxs-lookup"><span data-stu-id="650b0-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="650b0-435">Dokumenty z właściwości wieku równy toohello ciąg "21" lub ciąg hello "0021", nie będzie odpowiadała jako wyrażenie hello "21" = 21 ocenia tooundefined.</span><span class="sxs-lookup"><span data-stu-id="650b0-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="650b0-436">Umożliwia to lepsze wykorzystanie indeksów, ponieważ wyszukiwanie hello określonej wartości (np. numer 21) jest szybsze niż wyszukiwanie nieokreśloną liczbę potencjalnych (tj. liczba 21 lub ciągi "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="650b0-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="650b0-437">To różni się od sposobu JavaScript ocenia operatory na wartości różnych typów.</span><span class="sxs-lookup"><span data-stu-id="650b0-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="650b0-438">**Porównanie i równości obiektów i tablic**</span><span class="sxs-lookup"><span data-stu-id="650b0-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="650b0-439">Porównywanie tablicy lub obiekt wartości przy użyciu operatorów zakresu (>, > =, <, < =) spowoduje niezdefiniowana, ponieważ nie ma nie kolejności zdefiniowane dla obiektu ani tablicy wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="650b0-440">Jednak przy użyciu operatorów równości i nierówności (=,! =, <>) jest obsługiwana i będzie można porównać wartości strukturę.</span><span class="sxs-lookup"><span data-stu-id="650b0-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="650b0-441">Tablice są takie same, jeśli obie tablice mają tę samą liczbę elementów, a elementy w pozycji dopasowania również są takie same.</span><span class="sxs-lookup"><span data-stu-id="650b0-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="650b0-442">Jeśli porównanie jakiejkolwiek parze elementów powoduje Niezdefiniowany, hello wynik porównania tablicy nie jest zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="650b0-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="650b0-443">Obiekty są takie same, jeśli oba obiekty mają takie same właściwości zdefiniowane, a także są takie same wartości dopasowania właściwości.</span><span class="sxs-lookup"><span data-stu-id="650b0-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="650b0-444">Jeśli porównanie każdej pary wartości właściwości powoduje Niezdefiniowany, hello wynik porównania obiektu jest zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="650b0-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="650b0-445"><a name="bk_constants"></a>Stałe</span><span class="sxs-lookup"><span data-stu-id="650b0-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="650b0-446">Stała, znana także jako literału lub wartość skalarną, to symbol, który reprezentuje wartość określonych danych.</span><span class="sxs-lookup"><span data-stu-id="650b0-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="650b0-447">format Hello stałej zależy od typu danych hello hello wartość, która reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="650b0-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="650b0-448">**Obsługiwane typy skalarne danych:**</span><span class="sxs-lookup"><span data-stu-id="650b0-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="650b0-449">**Typ**</span><span class="sxs-lookup"><span data-stu-id="650b0-449">**Type**</span></span>|<span data-ttu-id="650b0-450">**Kolejność wartości**</span><span class="sxs-lookup"><span data-stu-id="650b0-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="650b0-451">**Niezdefiniowana**</span><span class="sxs-lookup"><span data-stu-id="650b0-451">**Undefined**</span></span>|<span data-ttu-id="650b0-452">Pojedyncza wartość: **niezdefiniowane**</span><span class="sxs-lookup"><span data-stu-id="650b0-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="650b0-453">**Wartość null**</span><span class="sxs-lookup"><span data-stu-id="650b0-453">**Null**</span></span>|<span data-ttu-id="650b0-454">Pojedyncza wartość: **wartości null**</span><span class="sxs-lookup"><span data-stu-id="650b0-454">Single value: **null**</span></span>|  
|<span data-ttu-id="650b0-455">**Wartość logiczna**</span><span class="sxs-lookup"><span data-stu-id="650b0-455">**Boolean**</span></span>|<span data-ttu-id="650b0-456">Wartości: **false**, **true**.</span><span class="sxs-lookup"><span data-stu-id="650b0-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="650b0-457">**Numer**</span><span class="sxs-lookup"><span data-stu-id="650b0-457">**Number**</span></span>|<span data-ttu-id="650b0-458">Liczba podwójnej precyzji liczb zmiennoprzecinkowych, IEEE-754 standardowa.</span><span class="sxs-lookup"><span data-stu-id="650b0-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="650b0-459">**Ciąg**</span><span class="sxs-lookup"><span data-stu-id="650b0-459">**String**</span></span>|<span data-ttu-id="650b0-460">Sekwencja zero lub więcej znaków Unicode.</span><span class="sxs-lookup"><span data-stu-id="650b0-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="650b0-461">Ciągi, musi być ujęty w pojedynczym lub podwójnym cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="650b0-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="650b0-462">**Tablica**</span><span class="sxs-lookup"><span data-stu-id="650b0-462">**Array**</span></span>|<span data-ttu-id="650b0-463">Sekwencja zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="650b0-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="650b0-464">Każdy element może być wartością dowolnego typu danych skalarnych, z wyjątkiem Undefined.</span><span class="sxs-lookup"><span data-stu-id="650b0-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="650b0-465">**Obiekt**</span><span class="sxs-lookup"><span data-stu-id="650b0-465">**Object**</span></span>|<span data-ttu-id="650b0-466">Nieuporządkowaną zestaw par nazwa/wartość zero lub więcej.</span><span class="sxs-lookup"><span data-stu-id="650b0-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="650b0-467">Nazwa jest ciągiem Unicode, wartość może być dowolnego typu danych skalarnych, z wyjątkiem **niezdefiniowane**.</span><span class="sxs-lookup"><span data-stu-id="650b0-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="650b0-468">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="650b0-469">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="650b0-470">Reprezentuje niezdefiniowana wartość typu Undefined.</span><span class="sxs-lookup"><span data-stu-id="650b0-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="650b0-471">Reprezentuje **null** wartości typu **Null**.</span><span class="sxs-lookup"><span data-stu-id="650b0-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="650b0-472">Reprezentuje stała typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="650b0-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="650b0-473">Reprezentuje **false** wartość typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="650b0-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="650b0-474">Reprezentuje **true** wartość typu Boolean.</span><span class="sxs-lookup"><span data-stu-id="650b0-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="650b0-475">Reprezentuje stałą.</span><span class="sxs-lookup"><span data-stu-id="650b0-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="650b0-476">Literałów dziesiętnych są liczbami reprezentowanej przy użyciu notacji dziesiętnej lub wykładniczej.</span><span class="sxs-lookup"><span data-stu-id="650b0-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="650b0-477">Literały szesnastkowe są przedstawiane za pomocą prefiks '0 x' następuje co najmniej jedną cyfrę szesnastkową liczby.</span><span class="sxs-lookup"><span data-stu-id="650b0-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="650b0-478">Reprezentuje stałą typu String.</span><span class="sxs-lookup"><span data-stu-id="650b0-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="650b0-479">Literały ciągu są reprezentowane przez sekwencję zero lub więcej znaków Unicode lub sekwencji unikowych ciągów Unicode.</span><span class="sxs-lookup"><span data-stu-id="650b0-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="650b0-480">Literały ciągu są ujęte w apostrofy (apostrof: ") lub podwójne cudzysłowy (cudzysłów:").</span><span class="sxs-lookup"><span data-stu-id="650b0-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="650b0-481">Dopuszczalne są następujące sekwencje unikowe:</span><span class="sxs-lookup"><span data-stu-id="650b0-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="650b0-482">**Sekwencja specjalna**</span><span class="sxs-lookup"><span data-stu-id="650b0-482">**Escape sequence**</span></span>|<span data-ttu-id="650b0-483">**Opis**</span><span class="sxs-lookup"><span data-stu-id="650b0-483">**Description**</span></span>|<span data-ttu-id="650b0-484">**Znak Unicode**</span><span class="sxs-lookup"><span data-stu-id="650b0-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="650b0-485">\\'</span><span class="sxs-lookup"><span data-stu-id="650b0-485">\\'</span></span>|<span data-ttu-id="650b0-486">apostrof (')</span><span class="sxs-lookup"><span data-stu-id="650b0-486">apostrophe (')</span></span>|<span data-ttu-id="650b0-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="650b0-487">U+0027</span></span>|  
|<span data-ttu-id="650b0-488">\\"</span><span class="sxs-lookup"><span data-stu-id="650b0-488">\\"</span></span>|<span data-ttu-id="650b0-489">znak cudzysłowu (")</span><span class="sxs-lookup"><span data-stu-id="650b0-489">quotation mark (")</span></span>|<span data-ttu-id="650b0-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="650b0-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="650b0-491">Odwrotna kreska ułamkowa (\\)</span><span class="sxs-lookup"><span data-stu-id="650b0-491">reverse solidus (\\)</span></span>|<span data-ttu-id="650b0-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="650b0-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="650b0-493">kreska ułamkowa (/)</span><span class="sxs-lookup"><span data-stu-id="650b0-493">solidus (/)</span></span>|<span data-ttu-id="650b0-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="650b0-494">U+002F</span></span>|  
|<span data-ttu-id="650b0-495">\b</span><span class="sxs-lookup"><span data-stu-id="650b0-495">\b</span></span>|<span data-ttu-id="650b0-496">BACKSPACE</span><span class="sxs-lookup"><span data-stu-id="650b0-496">backspace</span></span>|<span data-ttu-id="650b0-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="650b0-497">U+0008</span></span>|  
|<span data-ttu-id="650b0-498">\f</span><span class="sxs-lookup"><span data-stu-id="650b0-498">\f</span></span>|<span data-ttu-id="650b0-499">Wysuw strony</span><span class="sxs-lookup"><span data-stu-id="650b0-499">form feed</span></span>|<span data-ttu-id="650b0-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="650b0-500">U+000C</span></span>|  
|\n|<span data-ttu-id="650b0-501">wysuwu wiersza</span><span class="sxs-lookup"><span data-stu-id="650b0-501">line feed</span></span>|<span data-ttu-id="650b0-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="650b0-502">U+000A</span></span>|  
|<span data-ttu-id="650b0-503">\r</span><span class="sxs-lookup"><span data-stu-id="650b0-503">\r</span></span>|<span data-ttu-id="650b0-504">Powrót karetki</span><span class="sxs-lookup"><span data-stu-id="650b0-504">carriage return</span></span>|<span data-ttu-id="650b0-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="650b0-505">U+000D</span></span>|  
|<span data-ttu-id="650b0-506">\t</span><span class="sxs-lookup"><span data-stu-id="650b0-506">\t</span></span>|<span data-ttu-id="650b0-507">Karta</span><span class="sxs-lookup"><span data-stu-id="650b0-507">tab</span></span>|<span data-ttu-id="650b0-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="650b0-508">U+0009</span></span>|  
|<span data-ttu-id="650b0-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="650b0-509">\uXXXX</span></span>|<span data-ttu-id="650b0-510">Znak Unicode, zdefiniowane przez 4 cyfr szesnastkowych.</span><span class="sxs-lookup"><span data-stu-id="650b0-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="650b0-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="650b0-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="650b0-512"><a name="bk_query_perf_guidelines"></a>Wskazówki dotyczące wydajności kwerendy</span><span class="sxs-lookup"><span data-stu-id="650b0-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="650b0-513">Aby toobe zapytanie, wykonywane wydajnie dla dużych kolekcji powinien on używać filtrów, które mogą być przekazywane za pośrednictwem jednego lub kilku indeksów.</span><span class="sxs-lookup"><span data-stu-id="650b0-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="650b0-514">Indeks wyszukiwania będzie mogła zostać usunięta Hello następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="650b0-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="650b0-515">Za pomocą operatora równości (=) wyrażenie ścieżki dokumentu i stałą.</span><span class="sxs-lookup"><span data-stu-id="650b0-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="650b0-516">Operatory zakresu (<, \<=, >, > =) z wyrażenie ścieżki dokumentu i number — stałe.</span><span class="sxs-lookup"><span data-stu-id="650b0-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="650b0-517">Wyrażenie ścieżki dokumentu oznacza dowolne wyrażenie, które identyfikuje ścieżkę stałej w dokumentach hello z hello odwołuje się do bazy danych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="650b0-518">**Wyrażenie ścieżki dokumentu**</span><span class="sxs-lookup"><span data-stu-id="650b0-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="650b0-519">Wyrażenia ścieżki dokumentu są wyrażenia który ścieżki właściwości lub tablicy oceniających indeksatora za pośrednictwem dokumentu pochodzące z bazy danych kolekcji dokumentów.</span><span class="sxs-lookup"><span data-stu-id="650b0-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="650b0-520">Ta ścieżka może być używane tooidentify lokalizację hello wartości filtru bezpośrednio z poziomu hello dokumentów w kolekcji z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="650b0-521">Aby toobe wyrażenie traktowane jako wyrażenie ścieżki dokumentu powinno:</span><span class="sxs-lookup"><span data-stu-id="650b0-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="650b0-522">Odwołanie hello kolekcji głównego bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="650b0-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="650b0-523">Indeksator odwołanie do właściwości lub stała tablicy niektóre wyrażenia ścieżki dokumentu</span><span class="sxs-lookup"><span data-stu-id="650b0-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="650b0-524">Odwołanie alias, który reprezentuje wyrażenie ścieżki niektórych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="650b0-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="650b0-525">**Konwencje składni**</span><span class="sxs-lookup"><span data-stu-id="650b0-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="650b0-526">Witaj w poniższej tabeli opisano składnię toodescribe używane konwencje hello w odwołaniu do hello język zapytań usługi DocumentDB interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="650b0-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="650b0-527">**Konwencja**</span><span class="sxs-lookup"><span data-stu-id="650b0-527">**Convention**</span></span>|<span data-ttu-id="650b0-528">**Używany do**</span><span class="sxs-lookup"><span data-stu-id="650b0-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="650b0-529">WIELKIE LITERY</span><span class="sxs-lookup"><span data-stu-id="650b0-529">UPPERCASE</span></span>|<span data-ttu-id="650b0-530">Słowa kluczowe bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="650b0-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="650b0-531">małe litery</span><span class="sxs-lookup"><span data-stu-id="650b0-531">lowercase</span></span>|<span data-ttu-id="650b0-532">Słowa kluczowe z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="650b0-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="650b0-533">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="650b0-533">\<nonterminal></span></span>|<span data-ttu-id="650b0-534">Nonterminal, definiowane osobno.</span><span class="sxs-lookup"><span data-stu-id="650b0-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="650b0-535">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="650b0-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="650b0-536">Definicja składni hello nonterminal.</span><span class="sxs-lookup"><span data-stu-id="650b0-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="650b0-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="650b0-537">other_terminal</span></span>|<span data-ttu-id="650b0-538">Terminali (token) opisano szczegółowo w wyrazy.</span><span class="sxs-lookup"><span data-stu-id="650b0-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="650b0-539">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="650b0-539">identifier</span></span>|<span data-ttu-id="650b0-540">Identyfikator.</span><span class="sxs-lookup"><span data-stu-id="650b0-540">Identifier.</span></span> <span data-ttu-id="650b0-541">Umożliwia następujące znaki: a-z A-Z 0-9 _First znak nie może być cyfrą.</span><span class="sxs-lookup"><span data-stu-id="650b0-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="650b0-542">"string"</span><span class="sxs-lookup"><span data-stu-id="650b0-542">"string"</span></span>|<span data-ttu-id="650b0-543">Ciąg w cudzysłowie.</span><span class="sxs-lookup"><span data-stu-id="650b0-543">Quoted string.</span></span> <span data-ttu-id="650b0-544">Umożliwia dowolny prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-544">Allows any valid string.</span></span> <span data-ttu-id="650b0-545">Zobacz opis literał.</span><span class="sxs-lookup"><span data-stu-id="650b0-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="650b0-546">"symbol"</span><span class="sxs-lookup"><span data-stu-id="650b0-546">'symbol'</span></span>|<span data-ttu-id="650b0-547">Literał symbol, który jest częścią hello składni.</span><span class="sxs-lookup"><span data-stu-id="650b0-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="650b0-548">&#124; (pionowa kreska)</span><span class="sxs-lookup"><span data-stu-id="650b0-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="650b0-549">Alternatywy dla elementy składni.</span><span class="sxs-lookup"><span data-stu-id="650b0-549">Alternatives for syntax items.</span></span> <span data-ttu-id="650b0-550">Można użyć tylko jednej z określonych elementów hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="650b0-551">/(brackets)]</span><span class="sxs-lookup"><span data-stu-id="650b0-551">[ ] /(brackets)</span></span>|<span data-ttu-id="650b0-552">Nawiasy kwadratowe powinno być jeden lub więcej elementów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="650b0-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="650b0-553">[,.. .n]</span><span class="sxs-lookup"><span data-stu-id="650b0-553">[ ,...n ]</span></span>|<span data-ttu-id="650b0-554">Wskazuje, że hello poprzedzających elementu może być powtarzane n liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="650b0-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="650b0-555">wystąpienia Hello są oddzielone przecinkami.</span><span class="sxs-lookup"><span data-stu-id="650b0-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="650b0-556">[.. .n]</span><span class="sxs-lookup"><span data-stu-id="650b0-556">[ ...n ]</span></span>|<span data-ttu-id="650b0-557">Wskazuje, że hello poprzedzających elementu może być powtarzane n liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="650b0-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="650b0-558">wystąpienia Hello są rozdzielane puste wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="650b0-559"><a name="bk_built_in_functions"></a>Funkcje wbudowane</span><span class="sxs-lookup"><span data-stu-id="650b0-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="650b0-560">Azure DB rozwiązania Cosmos udostępnia wiele wbudowanych funkcji SQL.</span><span class="sxs-lookup"><span data-stu-id="650b0-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="650b0-561">Poniżej wymieniono kategorie Hello funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="650b0-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="650b0-562">Funkcja</span><span class="sxs-lookup"><span data-stu-id="650b0-562">Function</span></span>|<span data-ttu-id="650b0-563">Opis</span><span class="sxs-lookup"><span data-stu-id="650b0-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="650b0-564">Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="650b0-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="650b0-565">Witaj funkcje matematyczne każdego wykonywanie obliczeń, zwykle oparte na wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="650b0-566">Typ funkcji sprawdzania</span><span class="sxs-lookup"><span data-stu-id="650b0-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="650b0-567">Sprawdzanie, czy funkcje typu Hello pozwalają toocheck hello typ wyrażenia w obrębie zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="650b0-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="650b0-568">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="650b0-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="650b0-569">Funkcje ciągów Hello wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="650b0-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="650b0-570">Funkcje tablicy</span><span class="sxs-lookup"><span data-stu-id="650b0-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="650b0-571">Funkcje tablicy Hello wykonywać operacji na tablicy wartości wejściowej i przywracać liczbowych, wartość logiczną lub tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="650b0-572">Funkcje przestrzenne</span><span class="sxs-lookup"><span data-stu-id="650b0-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="650b0-573">Funkcje przestrzenne Hello wykonania operacji na wartości wejściowej obiektu przestrzennego i zwracać wartość liczbowa lub wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="650b0-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="650b0-574"><a name="bk_mathematical_functions"></a>Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="650b0-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="650b0-575">Witaj następujące funkcje wykonywanie obliczeń, zwykle oparte na wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="650b0-576">ABS</span><span class="sxs-lookup"><span data-stu-id="650b0-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="650b0-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="650b0-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="650b0-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="650b0-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="650b0-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="650b0-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="650b0-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="650b0-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="650b0-581">LIMITU</span><span class="sxs-lookup"><span data-stu-id="650b0-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="650b0-582">COS</span><span class="sxs-lookup"><span data-stu-id="650b0-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="650b0-583">KOT</span><span class="sxs-lookup"><span data-stu-id="650b0-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="650b0-584">STOPNI</span><span class="sxs-lookup"><span data-stu-id="650b0-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="650b0-585">EXP</span><span class="sxs-lookup"><span data-stu-id="650b0-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="650b0-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="650b0-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="650b0-587">DZIENNIK</span><span class="sxs-lookup"><span data-stu-id="650b0-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="650b0-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="650b0-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="650b0-589">PI</span><span class="sxs-lookup"><span data-stu-id="650b0-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="650b0-590">ZASILANIA</span><span class="sxs-lookup"><span data-stu-id="650b0-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="650b0-591">WARTOŚĆ W RADIANACH</span><span class="sxs-lookup"><span data-stu-id="650b0-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="650b0-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="650b0-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="650b0-593">SIN</span><span class="sxs-lookup"><span data-stu-id="650b0-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="650b0-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="650b0-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="650b0-595">KWADRATOWE</span><span class="sxs-lookup"><span data-stu-id="650b0-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="650b0-596">ZALOGUJ SIĘ</span><span class="sxs-lookup"><span data-stu-id="650b0-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="650b0-597">TAN</span><span class="sxs-lookup"><span data-stu-id="650b0-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="650b0-598">TRUNC —</span><span class="sxs-lookup"><span data-stu-id="650b0-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="650b0-599"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="650b0-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="650b0-600">Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-601">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-602">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-603">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-604">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-604">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-605">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-606">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-606">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-607">Witaj poniższy przykład przedstawia wyniki hello przy użyciu funkcji hello ABS na trzy różne liczby.</span><span class="sxs-lookup"><span data-stu-id="650b0-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="650b0-608">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="650b0-609"><a name="bk_acos"></a>ACOS</span><span class="sxs-lookup"><span data-stu-id="650b0-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="650b0-610">Zwraca hello kąt w radianach, którego cosinus jest hello określonego wyrażenia liczbowego. Skrót cosinus.</span><span class="sxs-lookup"><span data-stu-id="650b0-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="650b0-611">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-612">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-613">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-614">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-614">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-615">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-616">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-616">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-617">Witaj poniższy przykład zwraca hello ACOS-1.</span><span class="sxs-lookup"><span data-stu-id="650b0-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="650b0-618">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="650b0-619"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="650b0-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="650b0-620">Zwraca hello kąt w radianach, którego sinusem jest dana hello określony wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="650b0-621">Jest to również sinus.</span><span class="sxs-lookup"><span data-stu-id="650b0-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="650b0-622">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-623">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-624">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-625">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-625">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-626">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-627">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-627">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-628">Witaj poniższy przykład zwraca hello ASIN-1.</span><span class="sxs-lookup"><span data-stu-id="650b0-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="650b0-629">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="650b0-630"><a name="bk_atan"></a>ATAN</span><span class="sxs-lookup"><span data-stu-id="650b0-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="650b0-631">Zwraca hello kąt w radianach, którego tangens jest hello określony wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="650b0-632">Jest to również tangens.</span><span class="sxs-lookup"><span data-stu-id="650b0-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="650b0-633">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-634">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-635">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-636">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-636">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-637">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-638">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-638">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-639">Poniższy przykład, że zwraca hello ATAN hello Hello określona wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="650b0-640">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="650b0-641"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="650b0-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="650b0-642">Zwraca wartość główną hello hello arcus tangens y / x, wyrażone w radianach.</span><span class="sxs-lookup"><span data-stu-id="650b0-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="650b0-643">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-644">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-645">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-646">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-646">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-647">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-648">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-648">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-649">Witaj poniższy przykład oblicza hello ATN2 dla hello określony x i y składników.</span><span class="sxs-lookup"><span data-stu-id="650b0-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="650b0-650">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="650b0-651"><a name="bk_ceiling"></a>LIMITU</span><span class="sxs-lookup"><span data-stu-id="650b0-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="650b0-652">Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-653">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-654">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-655">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-656">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-656">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-657">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-658">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-658">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-659">Hello poniższy przykład przedstawia dodatnią liczbowe, ujemna, i wartości zerowe z hello limitu funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="650b0-660">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="650b0-661"><a name="bk_cos"></a>COS</span><span class="sxs-lookup"><span data-stu-id="650b0-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="650b0-662">Zwraca hello trygonometryczne cosinus hello określony kąt w radianach, w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="650b0-663">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-664">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-665">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-666">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-666">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-667">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-668">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-668">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-669">Poniższy przykład Hello oblicza hello COS hello określone kąta.</span><span class="sxs-lookup"><span data-stu-id="650b0-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="650b0-670">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="650b0-671"><a name="bk_cot"></a>KOT</span><span class="sxs-lookup"><span data-stu-id="650b0-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="650b0-672">Zwraca hello trygonometryczne cotangens hello określony kąt w radianach, w hello określonego wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-673">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-674">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-675">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-676">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-676">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-677">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-678">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-678">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-679">Poniższy przykład Hello oblicza hello KOT hello podanemu kątowi.</span><span class="sxs-lookup"><span data-stu-id="650b0-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="650b0-680">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="650b0-681"><a name="bk_degrees"></a>STOPNI</span><span class="sxs-lookup"><span data-stu-id="650b0-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="650b0-682">Zwraca hello odpowiadający mu kąt w stopniach dla kąta określonego w radianach.</span><span class="sxs-lookup"><span data-stu-id="650b0-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="650b0-683">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-684">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-685">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-686">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-686">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-687">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-688">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-688">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-689">Witaj poniższy przykład zwraca hello liczba stopni w kąta PI/2 radianów.</span><span class="sxs-lookup"><span data-stu-id="650b0-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="650b0-690">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="650b0-691"><a name="bk_floor"></a>FLOOR</span><span class="sxs-lookup"><span data-stu-id="650b0-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="650b0-692">Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-693">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-694">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-695">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-696">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-696">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-697">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-698">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-698">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-699">Hello poniższy przykład przedstawia dodatnią liczbowe, ujemna, i wartości zerowe z hello FLOOR — funkcja.</span><span class="sxs-lookup"><span data-stu-id="650b0-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="650b0-700">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="650b0-701"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="650b0-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="650b0-702">Zwraca hello wykładniczej wartość hello określona wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-703">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-704">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-705">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-706">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-706">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-707">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-708">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-708">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-709">Stała Hello **e** (2.718281...), jest hello podstawowej podstawę logarytmu naturalnego.</span><span class="sxs-lookup"><span data-stu-id="650b0-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="650b0-710">Witaj wykładnik liczby jest stała hello **e** wywoływane potęgi toohello liczba hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="650b0-711">Na przykład EXP(1.0) = e ^ 1.0 = 2.71828182845905 i EXP(10) = e ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="650b0-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="650b0-712">Hello wykładniczej z hello logarytm naturalny liczby jest liczba hello, sama: EXP (dziennik (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="650b0-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="650b0-713">I logarytm naturalny hello hello wykładnicza liczby jest liczba hello, sama: dziennika (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="650b0-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="650b0-714">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-714">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-715">Witaj poniższy przykład deklaruje zmienną i zwraca wartość wykładniczej hello hello określonej zmiennej (10).</span><span class="sxs-lookup"><span data-stu-id="650b0-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="650b0-716">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="650b0-717">Witaj poniższy przykład zwraca hello wykładniczej wartości logarytmu naturalnego hello 20 i logarytm naturalny hello hello wykładniczej 20.</span><span class="sxs-lookup"><span data-stu-id="650b0-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="650b0-718">Ponieważ te funkcje są funkcje odwrócone siebie, zwracana wartość hello z zaokrąglania zmiennoprzecinkowa matematyczne w obu przypadkach to 20.</span><span class="sxs-lookup"><span data-stu-id="650b0-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="650b0-719">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="650b0-720"><a name="bk_log"></a>DZIENNIK</span><span class="sxs-lookup"><span data-stu-id="650b0-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="650b0-721">Zwraca logarytm naturalny hello hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-722">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="650b0-723">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-724">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="650b0-725">Opcjonalny argument numeryczny, która ustawia hello jest podstawą logarytmu hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="650b0-726">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-726">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-727">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-728">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-728">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-729">Domyślnie LOG() Zwraca logarytm naturalny hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="650b0-730">Opcjonalny parametr podstawowego hello można zmienić base hello hello logarytm tooanother wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="650b0-731">logarytm naturalny Hello jest podstawowy toohello logarytm hello **e**, gdzie **e** jest nieracjonalnej stałej too2.718281828 przybliżeniu równe.</span><span class="sxs-lookup"><span data-stu-id="650b0-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="650b0-732">logarytm naturalny Hello hello wykładnicza liczby jest liczba hello, sama: dziennika (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="650b0-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="650b0-733">A hello wykładniczej z hello logarytm naturalny liczby jest liczbą hello, sama: EXP (dziennik (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="650b0-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="650b0-734">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-734">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-735">Witaj poniższy przykład deklaruje zmienną i zwraca wartość logarytmu hello hello określonej zmiennej (10).</span><span class="sxs-lookup"><span data-stu-id="650b0-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="650b0-736">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="650b0-737">Witaj poniższy przykład oblicza hello dziennika dla wykładnik hello liczby.</span><span class="sxs-lookup"><span data-stu-id="650b0-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="650b0-738">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="650b0-739"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="650b0-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="650b0-740">Zwraca logarytm base 10 hello hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-741">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-742">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-743">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-744">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-744">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-745">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-746">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="650b0-746">**Remarks**</span></span>  
  
 <span data-ttu-id="650b0-747">Witaj LOG10 i funkcje zasilania są tooone odwrotnie pokrewne innego.</span><span class="sxs-lookup"><span data-stu-id="650b0-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="650b0-748">Na przykład 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="650b0-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="650b0-749">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-749">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-750">Witaj poniższy przykład deklaruje zmienną i zwraca wartość LOG10 hello hello określonej zmiennej (100).</span><span class="sxs-lookup"><span data-stu-id="650b0-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="650b0-751">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="650b0-752"><a name="bk_pi"></a>PI</span><span class="sxs-lookup"><span data-stu-id="650b0-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="650b0-753">Zwraca hello stałą wartość PI.</span><span class="sxs-lookup"><span data-stu-id="650b0-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="650b0-754">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="650b0-755">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-756">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-757">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-757">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-758">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-759">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-759">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-760">Witaj poniższy przykład zwraca hello wartość PI.</span><span class="sxs-lookup"><span data-stu-id="650b0-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="650b0-761">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="650b0-762"><a name="bk_power"></a>ZASILANIA</span><span class="sxs-lookup"><span data-stu-id="650b0-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="650b0-763">Zwraca hello wartość hello określone wyrażenie toohello określony zasilania.</span><span class="sxs-lookup"><span data-stu-id="650b0-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="650b0-764">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="650b0-765">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-766">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="650b0-767">Jest hello zasilania toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="650b0-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="650b0-768">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-768">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-769">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-770">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-770">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-771">Hello poniższy przykład pokazuje, zwiększenie numeru zasilania toohello 3 (hello modułu liczby hello).</span><span class="sxs-lookup"><span data-stu-id="650b0-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="650b0-772">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="650b0-773"><a name="bk_radians"></a>WARTOŚĆ W RADIANACH</span><span class="sxs-lookup"><span data-stu-id="650b0-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="650b0-774">Zwraca wartość w radianach, po wprowadzeniu w stopniach, wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="650b0-775">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-776">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-777">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-778">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-778">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-779">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-780">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-780">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-781">Witaj poniższy przykład przyjmuje jako dane wejściowe kilka kąty i zwraca odpowiednimi wartościami radianach.</span><span class="sxs-lookup"><span data-stu-id="650b0-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="650b0-782">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="650b0-783"><a name="bk_round"></a>ROUND</span><span class="sxs-lookup"><span data-stu-id="650b0-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="650b0-784">Zwraca wartość liczbową zaokrąglony toohello najbliższej liczby całkowitej wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="650b0-785">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-786">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-787">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-788">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-788">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-789">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-790">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-790">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-791">Witaj poniższy przykład zaokrągla hello następującej liczby dodatnie i ujemne toohello najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="650b0-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="650b0-792">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="650b0-793"><a name="bk_sign"></a>ZALOGUJ SIĘ</span><span class="sxs-lookup"><span data-stu-id="650b0-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="650b0-794">Zwraca hello plus (+ 1) (0), lub znakiem minus (-1) z hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-795">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-796">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-797">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-798">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-798">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-799">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-800">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-800">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-801">Witaj poniższy przykład zwraca hello znak wartości liczb z too2-2.</span><span class="sxs-lookup"><span data-stu-id="650b0-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="650b0-802">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="650b0-803"><a name="bk_sin"></a>SIN</span><span class="sxs-lookup"><span data-stu-id="650b0-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="650b0-804">Zwraca hello trygonometryczne sinus hello określony kąt w radianach, w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="650b0-805">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-806">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-807">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-808">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-808">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-809">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-810">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-810">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-811">Poniższy przykład Hello oblicza hello SINUS określonego kąta hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="650b0-812">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="650b0-813"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="650b0-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="650b0-814">Zwraca pierwiastek kwadratowy hello hello określono wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="650b0-815">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-816">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-817">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-818">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-818">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-819">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-820">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-820">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-821">Witaj poniższy przykład zwraca pierwiastków kwadratowych hello liczb od 1 do 3.</span><span class="sxs-lookup"><span data-stu-id="650b0-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="650b0-822">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="650b0-823"><a name="bk_square"></a>KWADRATOWE</span><span class="sxs-lookup"><span data-stu-id="650b0-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="650b0-824">Zwraca hello kwadratowy z hello określono wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="650b0-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="650b0-825">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-826">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-827">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-828">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-828">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-829">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-830">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-830">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-831">Witaj poniższy przykład zwraca hello kwadratów liczb od 1 do 3.</span><span class="sxs-lookup"><span data-stu-id="650b0-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="650b0-832">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="650b0-833"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="650b0-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="650b0-834">Zwraca tangens hello hello określony kąt w radianach, w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="650b0-835">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-836">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-837">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-838">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-838">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-839">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-840">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-840">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-841">Witaj poniższy przykład oblicza tangens hello (PI) / 2.</span><span class="sxs-lookup"><span data-stu-id="650b0-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="650b0-842">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="650b0-843"><a name="bk_trunc"></a>TRUNC —</span><span class="sxs-lookup"><span data-stu-id="650b0-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="650b0-844">Zwraca wartość liczbową skróconą toohello najbliższą wartość całkowitą.</span><span class="sxs-lookup"><span data-stu-id="650b0-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="650b0-845">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="650b0-846">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="650b0-847">To wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-848">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-848">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-849">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-850">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-850">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-851">Poniższy przykład Hello obcina hello następującej liczby dodatnie i ujemne toohello najbliższej liczby całkowitej wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="650b0-852">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="650b0-853"><a name="bk_type_checking_functions"></a>Typ funkcji sprawdzania</span><span class="sxs-lookup"><span data-stu-id="650b0-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="650b0-854">Hello następujące funkcje obsługi typu sprawdzanie względem wartości wejściowe, a każdy zwracać wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="650b0-855">IS_ARRAY —</span><span class="sxs-lookup"><span data-stu-id="650b0-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="650b0-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="650b0-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="650b0-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="650b0-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="650b0-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="650b0-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="650b0-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="650b0-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="650b0-860">IS_OBJECT —</span><span class="sxs-lookup"><span data-stu-id="650b0-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="650b0-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="650b0-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="650b0-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="650b0-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="650b0-863"><a name="bk_is_array"></a>IS_ARRAY —</span><span class="sxs-lookup"><span data-stu-id="650b0-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="650b0-864">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest tablicą.</span><span class="sxs-lookup"><span data-stu-id="650b0-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="650b0-865">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="650b0-866">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-867">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-868">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-868">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-869">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-870">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-870">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-871">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg, wartość null, obiekt, tablicy i niezdefiniowane typów za pomocą hello is_array — funkcja.</span><span class="sxs-lookup"><span data-stu-id="650b0-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-872">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="650b0-873"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="650b0-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="650b0-874">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="650b0-875">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="650b0-876">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-877">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-878">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-878">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-879">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-880">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-880">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-881">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_BOOL funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-882">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="650b0-883"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="650b0-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="650b0-884">Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="650b0-885">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="650b0-886">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-887">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-888">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-888">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-889">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-890">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-890">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-891">powitania po przykład sprawdza obecność hello właściwości w hello określony dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="650b0-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="650b0-892">Witaj najpierw zwraca wartość true, ponieważ "a" jest obecny, ale hello drugi zwraca wartość false, ponieważ nie ma "b".</span><span class="sxs-lookup"><span data-stu-id="650b0-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="650b0-893">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="650b0-894"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="650b0-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="650b0-895">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="650b0-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="650b0-896">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="650b0-897">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-898">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-899">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-899">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-900">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-901">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-901">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-902">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_NULL funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-903">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="650b0-904"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="650b0-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="650b0-905">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest liczbą.</span><span class="sxs-lookup"><span data-stu-id="650b0-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="650b0-906">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="650b0-907">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-908">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-909">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-909">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-910">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-911">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-911">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-912">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_NULL funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-913">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="650b0-914"><a name="bk_is_object"></a>IS_OBJECT —</span><span class="sxs-lookup"><span data-stu-id="650b0-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="650b0-915">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest obiektem JSON.</span><span class="sxs-lookup"><span data-stu-id="650b0-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="650b0-916">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="650b0-917">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-918">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-919">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-919">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-920">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-921">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-921">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-922">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg, wartość null, obiekt, tablicy i niezdefiniowane typów za pomocą hello is_object — funkcja.</span><span class="sxs-lookup"><span data-stu-id="650b0-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-923">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="650b0-924"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="650b0-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="650b0-925">Zwraca wartość logiczną wskazującą, czy określony typ hello hello wyrażenie jest typu pierwotnego (string, Boolean, liczbowa lub wartość null).</span><span class="sxs-lookup"><span data-stu-id="650b0-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="650b0-926">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="650b0-927">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-928">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-929">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-929">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-930">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-931">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-931">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-932">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_PRIMITIVE funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-933">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="650b0-934"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="650b0-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="650b0-935">Zwraca wartość logiczną wskazującą, czy typ hello hello określone wyrażenie jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="650b0-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="650b0-936">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="650b0-937">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="650b0-938">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-939">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-939">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-940">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-941">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-941">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-942">Hello poniższy przykład sprawdza obiektów JSON Boolean, numer, ciąg null, obiektu, tablicy i niezdefiniowane typów za pomocą hello IS_STRING funkcji.</span><span class="sxs-lookup"><span data-stu-id="650b0-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="650b0-943">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="650b0-944"><a name="bk_string_functions"></a>Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="650b0-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="650b0-945">Witaj następujące funkcje skalarne wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="650b0-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="650b0-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="650b0-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="650b0-947">ZAWIERA</span><span class="sxs-lookup"><span data-stu-id="650b0-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="650b0-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="650b0-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="650b0-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="650b0-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="650b0-950">PO LEWEJ</span><span class="sxs-lookup"><span data-stu-id="650b0-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="650b0-951">DŁUGOŚĆ</span><span class="sxs-lookup"><span data-stu-id="650b0-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="650b0-952">NIŻSZE</span><span class="sxs-lookup"><span data-stu-id="650b0-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="650b0-953">PRZYTP</span><span class="sxs-lookup"><span data-stu-id="650b0-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="650b0-954">ZAMIEŃ</span><span class="sxs-lookup"><span data-stu-id="650b0-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="650b0-955">REPLIKUJ</span><span class="sxs-lookup"><span data-stu-id="650b0-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="650b0-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="650b0-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="650b0-957">PRAWO</span><span class="sxs-lookup"><span data-stu-id="650b0-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="650b0-958">PRZYTK</span><span class="sxs-lookup"><span data-stu-id="650b0-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="650b0-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="650b0-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="650b0-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="650b0-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="650b0-961">GÓRNY</span><span class="sxs-lookup"><span data-stu-id="650b0-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="650b0-962"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="650b0-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="650b0-963">Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="650b0-964">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="650b0-965">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-966">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-967">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-967">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-968">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-969">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-969">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-970">powitania po przykład zwraca ciąg hello połączonych hello określone wartości.</span><span class="sxs-lookup"><span data-stu-id="650b0-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="650b0-971">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="650b0-972"><a name="bk_contains"></a>ZAWIERA</span><span class="sxs-lookup"><span data-stu-id="650b0-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="650b0-973">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="650b0-974">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="650b0-975">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-976">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-977">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-977">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-978">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-979">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-979">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-980">Witaj poniższy przykład sprawdza, czy "abc" zawiera "ab" a "d".</span><span class="sxs-lookup"><span data-stu-id="650b0-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="650b0-981">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="650b0-982"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="650b0-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="650b0-983">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi.</span><span class="sxs-lookup"><span data-stu-id="650b0-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="650b0-984">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="650b0-985">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-986">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-987">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-987">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-988">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-989">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-989">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-990">Witaj poniższy przykład zwraca powitalne "abc" kończy się wyrazem "b" i "bc".</span><span class="sxs-lookup"><span data-stu-id="650b0-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="650b0-991">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="650b0-992"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="650b0-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="650b0-993">Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="650b0-994">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="650b0-995">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-996">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-997">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-997">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-998">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-999">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-999">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1000">Witaj poniższy przykład zwraca indeks hello różnych podciągów wewnątrz "abc".</span><span class="sxs-lookup"><span data-stu-id="650b0-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="650b0-1001">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="650b0-1002"><a name="bk_left"></a>PO LEWEJ</span><span class="sxs-lookup"><span data-stu-id="650b0-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="650b0-1003">Zwraca hello lewej części ciągu z hello określona liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="650b0-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="650b0-1004">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="650b0-1005">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1006">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="650b0-1007">Jest dowolne prawidłowe wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1008">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1009">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1010">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1010">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1011">Witaj poniższy przykład zwraca hello lewej części "abc" dla różnych wartości długości.</span><span class="sxs-lookup"><span data-stu-id="650b0-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="650b0-1012">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="650b0-1013"><a name="bk_length"></a>DŁUGOŚĆ</span><span class="sxs-lookup"><span data-stu-id="650b0-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="650b0-1014">Witaj zwraca liczbę znaków hello określone wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="650b0-1015">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1016">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1017">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1018">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1019">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1020">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1020">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1021">Witaj poniższy przykład zwraca hello długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="650b0-1022">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="650b0-1023"><a name="bk_lower"></a>NIŻSZE</span><span class="sxs-lookup"><span data-stu-id="650b0-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="650b0-1024">Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę.</span><span class="sxs-lookup"><span data-stu-id="650b0-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="650b0-1025">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1026">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1027">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1028">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1029">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1030">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1030">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1031">powitania po przykładzie pokazano, jak toouse małe w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="650b0-1032">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="650b0-1033"><a name="bk_ltrim"></a>PRZYTP</span><span class="sxs-lookup"><span data-stu-id="650b0-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="650b0-1034">Zwraca wyrażenie ciągu, po usuwa spacje wiodące.</span><span class="sxs-lookup"><span data-stu-id="650b0-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="650b0-1035">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1036">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1037">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1038">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1039">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1040">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1040">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1041">powitania po przykładzie pokazano, jak toouse LTRIM w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="650b0-1042">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="650b0-1043"><a name="bk_replace"></a>ZAMIEŃ</span><span class="sxs-lookup"><span data-stu-id="650b0-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="650b0-1044">Zamienia wszystkie wystąpienia określonej wartości ciągu na inną wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="650b0-1045">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="650b0-1046">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1047">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1048">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1049">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1050">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1050">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1051">Witaj poniższy przykład pokazuje, jak zastąpić toouse w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="650b0-1052">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="650b0-1053"><a name="bk_replicate"></a>REPLIKOWANIE</span><span class="sxs-lookup"><span data-stu-id="650b0-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="650b0-1054">Wartość ciągu jest powtarzany określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="650b0-1055">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="650b0-1056">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1057">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="650b0-1058">Jest dowolne prawidłowe wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1059">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1060">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1061">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1061">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1062">Witaj poniższy przykład przedstawia sposób REPLIKOWANIA toouse w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="650b0-1063">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="650b0-1064"><a name="bk_reverse"></a>REVERSE</span><span class="sxs-lookup"><span data-stu-id="650b0-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="650b0-1065">Zwraca hello odwrotna kolejność wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="650b0-1066">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1067">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1068">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1069">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1070">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1071">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1071">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1072">Witaj poniższy przykład pokazuje, jak toouse wstecznego w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="650b0-1073">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="650b0-1074"><a name="bk_right"></a>PRAWO</span><span class="sxs-lookup"><span data-stu-id="650b0-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="650b0-1075">Zwraca hello prawej części ciągu z hello określona liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="650b0-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="650b0-1076">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="650b0-1077">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1078">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="650b0-1079">Jest dowolne prawidłowe wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1080">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1081">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1082">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1082">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1083">Witaj poniższy przykład zwraca hello prawa część "abc" dla różnych wartości długości.</span><span class="sxs-lookup"><span data-stu-id="650b0-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="650b0-1084">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="650b0-1085"><a name="bk_rtrim"></a>PRZYTK</span><span class="sxs-lookup"><span data-stu-id="650b0-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="650b0-1086">Zwraca wyrażenie ciągu, po usuwa spacje końcowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="650b0-1087">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1088">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1089">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1090">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1091">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1092">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1092">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1093">powitania po przykładzie pokazano, jak toouse RTRIM w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="650b0-1094">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="650b0-1095"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="650b0-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="650b0-1096">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello rozpoczyna się od hello drugi.</span><span class="sxs-lookup"><span data-stu-id="650b0-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="650b0-1097">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="650b0-1098">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1099">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1100">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1101">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-1102">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1102">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1103">Witaj poniższy przykład sprawdza, czy hello ciągu "abc" rozpoczyna się od ciągu "b" i "a".</span><span class="sxs-lookup"><span data-stu-id="650b0-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="650b0-1104">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="650b0-1105"><a name="bk_substring"></a>SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="650b0-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="650b0-1106">Zwraca część wyrażenia ciągu, zaczynając od hello określono znaku na pozycji liczony od zera i kontynuuje toohello określone długości lub toohello końca ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="650b0-1107">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="650b0-1108">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1109">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="650b0-1110">Jest dowolne prawidłowe wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1111">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1112">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1113">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1113">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1114">Witaj poniższy przykład zwraca podciąg hello "abc" począwszy od 1 i o długości 1 znak.</span><span class="sxs-lookup"><span data-stu-id="650b0-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="650b0-1115">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="650b0-1116"><a name="bk_upper"></a>GÓRNY</span><span class="sxs-lookup"><span data-stu-id="650b0-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="650b0-1117">Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę.</span><span class="sxs-lookup"><span data-stu-id="650b0-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="650b0-1118">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="650b0-1119">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="650b0-1120">Jest dowolne wyrażenie prawidłowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="650b0-1121">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1122">Zwraca wyrażenie ciągu.</span><span class="sxs-lookup"><span data-stu-id="650b0-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="650b0-1123">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1123">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1124">powitania po przykładzie pokazano, jak toouse górna w kwerendzie</span><span class="sxs-lookup"><span data-stu-id="650b0-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="650b0-1125">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="650b0-1126"><a name="bk_array_functions"></a>Funkcje tablicy</span><span class="sxs-lookup"><span data-stu-id="650b0-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="650b0-1127">następujące funkcje skalarne Hello wykonania operacji na tablicy wartości wejściowej i powrotu liczbowego, wartość logiczną lub tablicy</span><span class="sxs-lookup"><span data-stu-id="650b0-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="650b0-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="650b0-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="650b0-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="650b0-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="650b0-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="650b0-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="650b0-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="650b0-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="650b0-1132"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="650b0-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="650b0-1133">Zwraca tablicę, która jest wynikiem hello łączenie dwóch lub więcej wartości tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="650b0-1134">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="650b0-1135">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="650b0-1136">Jest dowolne wyrażenie prawidłowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="650b0-1137">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1138">Zwraca wyrażenie tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="650b0-1139">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1139">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1140">Witaj następujący przykład sposobu tooconcatenate dwóch stałych.</span><span class="sxs-lookup"><span data-stu-id="650b0-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="650b0-1141">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="650b0-1142"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="650b0-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="650b0-1143">Zwraca wartość typu Boolean wskazującą, czy tablica hello zawiera hello określona wartość.</span><span class="sxs-lookup"><span data-stu-id="650b0-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="650b0-1144">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="650b0-1145">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="650b0-1146">Jest dowolne wyrażenie prawidłowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="650b0-1147">Jest dowolne prawidłowe wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="650b0-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="650b0-1148">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1149">Zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="650b0-1150">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1150">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1151">Poniższy przykład sposobu Hello toocheck członkostwa w tablicy przy użyciu ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="650b0-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="650b0-1152">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="650b0-1153"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="650b0-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="650b0-1154">Zwraca numer hello elementów hello określone wyrażenie tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="650b0-1155">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="650b0-1156">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="650b0-1157">Jest dowolne wyrażenie prawidłowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="650b0-1158">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1159">Zwraca wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="650b0-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1160">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1160">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1161">następujący przykład Witaj, jak tooget hello długość tablicy przy użyciu ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="650b0-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="650b0-1162">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="650b0-1163"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="650b0-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="650b0-1164">Zwraca część wyrażenie tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="650b0-1165">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="650b0-1166">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="650b0-1167">Jest dowolne wyrażenie prawidłowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="650b0-1168">Jest dowolne prawidłowe wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="650b0-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="650b0-1169">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1170">Zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="650b0-1171">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1171">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1172">Poniższy przykład sposobu Hello tooget część tablicy przy użyciu ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="650b0-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="650b0-1173">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="650b0-1174"><a name="bk_spatial_functions"></a>Funkcje przestrzenne</span><span class="sxs-lookup"><span data-stu-id="650b0-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="650b0-1175">Witaj następujące funkcje skalarne wykonania operacji na wartości wejściowej obiektu przestrzennego i zwracać wartość liczbowa lub wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="650b0-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="650b0-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="650b0-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="650b0-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="650b0-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="650b0-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="650b0-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="650b0-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="650b0-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="650b0-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="650b0-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="650b0-1181"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="650b0-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="650b0-1182">Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="650b0-1183">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="650b0-1184">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1185">Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="650b0-1186">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1187">Zwraca wartość wyrażenia liczbowego zawierający hello odległości.</span><span class="sxs-lookup"><span data-stu-id="650b0-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="650b0-1188">To wymaganie jest wyrażone w liczników dla systemu odniesienia hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="650b0-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="650b0-1189">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1189">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1190">powitania po przykładzie pokazano, jak tooreturn wszystkie dokumenty rodziny, które są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="650b0-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="650b0-1191">.</span><span class="sxs-lookup"><span data-stu-id="650b0-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="650b0-1192">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="650b0-1193"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="650b0-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="650b0-1194">Zwraca wyrażenie Boolean wskazującą, czy hello GeoJSON (punkt, wielokąta lub LineString) określony obiekt w pierwszym argumencie hello mieści hello GeoJSON (punkt, wielokąta lub LineString) hello drugi argument.</span><span class="sxs-lookup"><span data-stu-id="650b0-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="650b0-1195">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="650b0-1196">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1197">Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1198">Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="650b0-1199">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1200">Zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="650b0-1201">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1201">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1202">Witaj poniższy przykład pokazuje, jak toofind rodziny wszystkich dokumentów w ramach przy użyciu ST_WITHIN wielokąta.</span><span class="sxs-lookup"><span data-stu-id="650b0-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="650b0-1203">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="650b0-1204"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="650b0-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="650b0-1205">Zwraca wartość wskazującą, czy hello GeoJSON (punkt, wielokąta lub LineString) określony obiekt w pierwszym argumencie hello przecina hello GeoJSON (punkt, wielokąta lub LineString) w hello drugi argument wyrażenia logicznego.</span><span class="sxs-lookup"><span data-stu-id="650b0-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="650b0-1206">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="650b0-1207">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1208">Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1209">Jest dowolne prawidłowe wyrażenie obiektu GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="650b0-1210">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1211">Zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="650b0-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="650b0-1212">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1212">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1213">powitania po przykładzie pokazano, jak toofind wszystkich obszarów, które przecina z hello podany wielokąta.</span><span class="sxs-lookup"><span data-stu-id="650b0-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="650b0-1214">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="650b0-1215"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="650b0-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="650b0-1216">Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="650b0-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="650b0-1217">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="650b0-1218">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1219">Jest dowolne prawidłowe wyrażenie GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="650b0-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="650b0-1220">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1221">Zwraca wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="650b0-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="650b0-1222">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1222">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1223">powitania po przykładzie pokazano, jak toocheck, gdy punkt jest nieprawidłowy, przy użyciu ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="650b0-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="650b0-1224">Na przykład ten punkt ma wartość szerokości geograficznej, który nie jest prawidłowy zakres wartości [-90, 90] hello, więc hello zapytanie zwraca wartość false.</span><span class="sxs-lookup"><span data-stu-id="650b0-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="650b0-1225">W przypadku wielokątów hello GeoJSON specyfikacji wymaga hello ostatnią parę współrzędnych podane powinien hello sam jako pierwszy, toocreate hello zamknięty kształt.</span><span class="sxs-lookup"><span data-stu-id="650b0-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="650b0-1226">Punktów w wielokąta muszą być określone w kolejności przeciwnie do ruchu wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="650b0-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="650b0-1227">Wielokąt określony w kolejności zegara reprezentuje odwrotność hello hello regionu w niej.</span><span class="sxs-lookup"><span data-stu-id="650b0-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="650b0-1228">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="650b0-1229"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="650b0-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="650b0-1230">Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="650b0-1231">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="650b0-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="650b0-1232">**Argumenty**</span><span class="sxs-lookup"><span data-stu-id="650b0-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="650b0-1233">Jest dowolne GeoJSON prawidłowe wyrażenie punktu lub wielokąta.</span><span class="sxs-lookup"><span data-stu-id="650b0-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="650b0-1234">**Zwracane typy**</span><span class="sxs-lookup"><span data-stu-id="650b0-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="650b0-1235">Zwraca wartość JSON zawierający wartość logiczną w przypadku hello określony punkt GeoJSON lub wyrażenie wielokąta jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="650b0-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="650b0-1236">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="650b0-1236">**Examples**</span></span>  
  
 <span data-ttu-id="650b0-1237">Poniższy przykład sposobu Hello ważności toocheck (ze szczegółami) przy użyciu ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="650b0-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="650b0-1238">Oto hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="650b0-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="650b0-1239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="650b0-1239">Next steps</span></span>  
 <span data-ttu-id="650b0-1240">[Składnia SQL i kwerendy SQL dla bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="650b0-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="650b0-1241">Dokumentację platformy Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="650b0-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
