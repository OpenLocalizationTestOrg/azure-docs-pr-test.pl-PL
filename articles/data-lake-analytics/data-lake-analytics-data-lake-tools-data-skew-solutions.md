---
title: "aaaResolve problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Potencjalne rozwiązania problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Rozwiązywanie problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio

## <a name="what-is-data-skew"></a>Co to są dane pochylanie?

Krótko już wspomniano, Pochylenie danych jest nadmiernie reprezentowanego wartością. Załóżmy, że została przypisana 50 ekspertami podatku deklaracji podatkowych tooaudit, jeden egzaminator dla każdego stanu Stanów Zjednoczonych. Egzaminator Wyoming Hello, ponieważ hello wypełniania jest mały, ma małego toodo. W Kalifornijskiej jednak egzaminator hello jest przechowywana bardzo zajęty z powodu dużej populacji hello stanu.
    ![Przykład danych zegara problemu](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

W naszym scenariuszu danych hello nierównomiernie obejmowała wszystkie ekspertami podatku, co oznacza, że niektóre ekspertami musi działać więcej niż inne. W własne stanowisko często występują sytuacjach, takich jak hello egzaminator podatku w tym przykładzie. W sposób bardziej technicznych jednego wierzchołka pobiera znacznie więcej danych niż jego elementów równorzędnych sytuacji, która sprawia, że wierzchołków hello działać więcej niż hello inne osoby i który ostatecznie spowalnia całego zadania. Co to jest gorsza, hello zadania może się nie powieść, ponieważ wierzchołków może być, na przykład ograniczenie 5-godzinnym środowiska uruchomieniowego i ograniczenie 6 GB pamięci.

## <a name="resolving-data-skew-problems"></a>Rozwiązywanie problemów z danych zegara

Azure Data Lake Tools dla programu Visual Studio może pomóc wykryć, czy zadanie ma problem zegara danych. Jeśli istnieje problem, można rozwiązać go za pomocą rozwiązań hello w tej sekcji.

## <a name="solution-1-improve-table-partitioning"></a>Rozwiązanie 1: Poprawić, Partycjonowanie tabel

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Opcja 1: Hello filtru niesymetryczna wartość klucza z wyprzedzeniem

Jeśli nie ma ona wpływu na logice biznesowej, można filtrować hello wyższa częstotliwość wartości z wyprzedzeniem. Na przykład jeśli istnieje wiele 000 000 000 w kolumnie identyfikator GUID, nie możesz tooaggregate tej wartości. Przed agregacji, można wpisać "WHERE GUID! ="ruch 000 000 000"" toofilter hello wysokiej częstotliwości wartość.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Opcja 2: Wybierz inny klucz partycji lub dystrybucji

W hello poprzedzających przykład jeśli chcesz tylko toocheck hello inspekcji podatku obciążenia wszystkie za pośrednictwem hello kraju, hello danych dystrybucji można zwiększyć, wybierając numer identyfikacyjny hello jako klucz. Pobrania różnych partycji lub klucza dystrybucji można czasami dystrybucji hello danych bardziej równomiernie, ale należy się upewnić, że ten wybór nie ma wpływu na logice biznesowej toomake. Na przykład toocalculate hello podatku Suma dla każdego stanu może być toodesignate _stanu_ jako klucza partycji hello. Jeśli będziesz kontynuować tooexperience ten problem, spróbuj użyć opcja 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Opcja 3: Dodaj więcej partycji lub dystrybucji kluczy

Zamiast używać tylko _stanu_ jako klucza partycji, można użyć więcej niż jednego klucza do partycjonowania. Na przykład, Rozważ dodanie _kod POCZTOWY_ jako dodatkowa partycja partycji danych klucza tooreduce rozmiary i bardziej równomierne hello danych.

### <a name="option-4-use-round-robin-distribution"></a>Opcja 4: Użycie rozdzielanie

Jeśli nie możesz znaleźć odpowiedniego klucza partycji i dystrybucji, można spróbować rozdzielaniem toouse. Rozdzielanie traktuje wszystkie wiersze jednakowo i losowo umieszcza je w odpowiednich zasobników. pobiera równomiernego Hello danych, ale utraty miejscowości informacji zwrotnych, może również zmniejszyć wydajność zadania dla niektórych operacji. Ponadto, jeśli mimo to czynności agregacji dla klucza spowodowałoby zafałszowanie hello hello zegara danych problem zostanie będzie się powtarzał. toolearn więcej informacji na temat rozdzielanie, zobacz dystrybucje tabeli U-SQL hello sekcji [CREATE TABLE (U-SQL): Tworzenie tabeli ze schematem](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>2 — rozwiązanie: Poprawy hello planu zapytania

### <a name="option-1-use-hello-create-statistics-statement"></a>Opcja 1: Użycie instrukcji CREATE STATISTICS hello

U-SQL zawiera instrukcję CREATE STATISTICS hello w tabelach. Ta instrukcja daje więcej Optymalizator zapytań toohello informacji o hello właściwości danych, np. rozkład wartości, które są przechowywane w tabeli. Dla większości zapytań Optymalizator zapytań hello generuje już hello statystyki niezbędne dla planu zapytania wysokiej jakości. Czasami może być konieczne tooimprove wydajność zapytań, tworząc dodatkowe statystyki z instrukcji CREATE STATISTICS lub modyfikując hello projektu zapytania. Aby uzyskać więcej informacji, zobacz hello [instrukcji CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) strony.

Przykład kodu:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Statystyki informacje nie są automatycznie aktualizowane. Po zaktualizowaniu hello dane w tabeli bez ponownego utworzenia statystyki hello może zmniejszyć wydajność kwerend hello.

### <a name="option-2-use-skewfactor"></a>Opcja 2: Użycie SKEWFACTOR

Jeśli chcesz toosum hello podatkowych dla każdego stanu, należy użyć Grupuj według stanu, metody, która nie uniknąć hello zegara danych. Jednak może podać wskazówkę danych w tooidentify Twojego zapytania, które danych pochylanie w kluczach, dzięki czemu Optymalizator hello można przygotować plan wykonania.

Zazwyczaj można ustawić parametru hello jako 0,5 i 1, 0,5 oznacza nie dużo zegara duże znaczenie pochylenia i 1. Ponieważ wskazówka hello wpływa na plan wykonania optymalizacji dla bieżącej instrukcji hello i wszystkie podrzędne instrukcje, należy się wskazówka hello tooadd przed hello potencjalne niesymetryczna key-wise agregacji.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Przykład kodu:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Opcja 3: Użycie ROWCOUNT  
Ponadto tooSKEWFACTOR dla określonych niesymetryczna klucza join przypadków, jeśli wiadomo, że hello innych zestawu wierszy sprzężonych jest mały, można ustawić Optymalizator hello przez dodanie wskazówkę liczby wierszy w instrukcji U-SQL hello przed sprzężenia. W ten sposób Optymalizator można wybrać toohelp strategii emisji sprzężenia zwiększenia wydajności. Należy pamiętać, ROWCOUNT nie rozwiązania problemu zegara danych hello, że można zaoferować niektórych uzyskać dodatkową pomoc.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Przykład kodu:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Rozwiązanie 3: Poprawa hello reduktor zdefiniowane przez użytkownika i łączenia

Czasami może zapisywać toodeal zdefiniowanego przez użytkownika, z logiką skomplikowany proces i dobrze napisane reduktor i łączenia może ograniczyć problem zegara danych w niektórych przypadkach.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Opcja 1: Użycie reduktor rekursywny, jeśli to możliwe

Domyślnie reduktor zdefiniowane przez użytkownika jest uruchamiana w trybie niecykliczne, co oznacza, że zmniejszyć pracy dla klucza jest dystrybuowana do jednego wierzchołka. Jednak jeśli danych jest niesymetryczna, hello dużych zestawów danych może być przetwarzane w jednym wierzchołka i uruchom przez długi czas.

wydajność tooimprove, można dodać atrybutu w Twojej kodu toodefine reduktor toorun w trybie cykliczne. Następnie hello dużych zestawów danych można wierzchołków toomultiple rozproszone i uruchom równolegle, co przyspiesza swoją pracę.

toochange toorecursive reduktor niecykliczne należy toomake się, że Twoje algorytm asocjacyjnej. Na przykład Suma hello jest asocjacyjnej i medianę hello nie jest. Należy się upewnić, że hello danych wejściowych i wyjściowych dla reduktor zachować hello toomake tego samego schematu.

Atrybut reduktor cykliczne:

    [SqlUserDefinedReducer(IsRecursive = true)]

Przykład kodu:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Opcja 2: W trybie łączenia na poziomie wiersza, jeśli to możliwe

Wskazówki ROWCOUNT podobne toohello przypadków określonego klucza niesymetryczna sprzężenia, tryb łączenia próbuje toodistribute wartość klucza niesymetryczna ogromnych zestawów toomultiple wierzchołków tak, aby hello pracy mogą być wykonywane jednocześnie. Tryb łączenia nie można rozpoznać danych zegara problemów, ale mogą oferować niektórych uzyskać dodatkową pomoc na wartość klucza niesymetryczna ogromnych zestawów.

Domyślnie tryb łączenia hello jest pełny, co oznacza, że hello pozostałych zestawu wierszy i prawego wiersza zestawu nie mogą być oddzielone. Ustawianie trybu hello jako wewnętrzny/prawej/lewej umożliwia sprzężenia na poziomie wiersza. Hello system oddziela hello odpowiednich zestawów wierszy i rozpowszechnia je do wielu wierzchołków, które są uruchamiane równolegle. Jednak przed skonfigurowaniem trybie łączenia hello należy zachować ostrożność, że mogą być oddzielone tooensure, który hello odpowiednich zestawów wierszy.

przykład Witaj, który następuje zawiera zestaw rozdzielonych wiersza po lewej stronie. Każdy wiersz danych wyjściowych zależy pojedynczy wiersz wejściowych od lewej hello oraz potencjalnie zależy od wszystkich wierszy z hello prawo z hello takie same wartości klucza. Po ustawieniu trybu łączenia powitania od lewej systemu hello oddziela hello ogromnych lewej-zestawu wierszy w małych sieci i przypisuje je toomultiple wierzchołków.

![Ilustracja trybie łączenia](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Jeśli ustawisz hello łączenia nieprawidłowy tryb kombinacja hello jest mniej wydajne i hello wyniki mogą być nieprawidłowe.

Atrybuty trybu łączenia:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): W pojedynczym wierszu wejściowych od lewej hello zależy od każdego wiersza danych wyjściowych (i potencjalnie wszystkie wiersze z tabeli hello prawo z hello sama wartość klucza).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z prawej hello (i potencjalnie wszystkie wiersze z tabeli po lewej hello z hello sama wartość klucza).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z lewej hello i hello prawo z hello takie same wartości.

Przykład kodu:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
