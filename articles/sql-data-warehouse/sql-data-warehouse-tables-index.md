---
title: "tabele aaaIndexing w usłudze SQL Data Warehouse | Microsoft Azure"
description: "Wprowadzenie do korzystania z tabeli indeksowanie w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indeksowanie tabel w usłudze SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Typy danych][Data Types]
> * [Dystrybuuj][Distribute]
> * [Indeks][Index]
> * [Partycji][Partition]
> * [Statystyki][Statistics]
> * [Tymczasowe][Temporary]
> 
> 

Magazyn danych SQL oferuje kilka opcji indeksowania tym [klastrowane indeksy magazynu kolumn][clustered columnstore indexes], [klastrowane indeksy i nieklastrowanych indeksów] [ clustered indexes and nonclustered indexes].  Ponadto zapewnia ona również nie opcji indeksu znanej także jako [sterty][heap].  W tym artykule obejmuje korzyści hello każdego typu indeksu także porady toogetting hello większość wydajności poza z indeksów. Zobacz [Tworzenie tabeli składni] [ create table syntax] uzyskać więcej szczegółowych informacji na temat toocreate tabeli w usłudze SQL Data Warehouse.

## <a name="clustered-columnstore-indexes"></a>Klastrowane indeksy magazynu kolumn
Domyślnie usługi SQL Data Warehouse tworzy klastrowany indeks magazynu kolumn, czy nie indeksu określono opcji dla tabeli. Tabel klastrowanego magazynu kolumn oferują zarówno hello najwyższy poziom kompresji danych, a także najlepszą ogólną wydajność zapytań hello.  Tabel klastrowanego magazynu kolumn będą zazwyczaj przewyższyć klastrowanego indeksu lub sterty tabel i są zwykle najlepszym wyborem hello dużych tabel.  Z tego względu klastrowanego magazynu kolumn jest hello najlepsze toostart miejsce, gdy wiadomo, jak tooindex tabeli.  

toocreate klastrowanego magazynu kolumn tabeli, po prostu określić KLASTROWANY indeks magazynu kolumn w klauzuli WITH hello, lub pozostaw klauzuli WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Istnieje kilka scenariuszy, w którym klastrowanego magazynu kolumn nie może być dobrym rozwiązaniem:

* Tabele magazynu kolumn nie obsługują varchar(max), nvarchar(max) i varbinary(max).  Zamiast tego należy rozważyć stosu lub indeksu klastrowanego.
* Tabele magazynu kolumn mogą być mniej wydajne przejściowej danych.  Należy wziąć pod uwagę sterty, a czasami nawet tymczasowych tabel.
* Mała tabele zawierające mniej niż 100 milionów wierszy.  Należy wziąć pod uwagę sterty tabel.

## <a name="heap-tables"></a>Tabele sterty
Gdy dane są tymczasowo kierowanych na SQL Data Warehouse, może się okazać, że przy użyciu tabeli sterty dokona szybciej hello całego procesu.  Jest to spowodowane tooheaps obciążenia są szybsze niż tabele tooindex i w niektórych przypadkach hello można wykonać kolejne odczytu z pamięci podręcznej.  Przypadku ładowania danych toostage tylko przed uruchomieniem więcej przekształcenia, ładowanie hello tooheap tabeli będzie znacznie szybsze niż ładowania tooa danych hello klastrowanego magazynu kolumn tabeli. Ponadto podczas ładowania danych tooa [tabeli tymczasowej] [ Temporary] również załaduje znacznie szybciej niż ładowania magazynu toopermanent tabeli.  

Dla tabel odnośników małych, wiersze mniej niż 100 milionów często sterty tabel sensu.  Klastra magazynu kolumn tabel rozpocząć tooachieve optymalnej kompresji po więcej niż 100 milionów wierszy.

toocreate tabeli sterty, po prostu określić STERTY w klauzuli WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Klastrowanych i nieklastrowanych indeksów
Indeksy klastrowane może przewyższyć tabel klastrowanego magazynu kolumn, gdy pojedynczy wiersz musi toobe szybko pobrać.  Dla zapytania, gdy jeden lub kilka bardzo wyszukiwania wiersza jest wymagane tooperformance z najwyższą szybkości należy wziąć pod uwagę indeksu klastra lub dodatkowej indeks nieklastrowany.  Witaj wadą toousing indeks klastrowany jest skorzystają tylko zapytania, które korzystać z wysokiej selektywnego filtru hello indeksu klastrowanego kolumna.  Filtr tooimprove na innych kolumn indeksu nieklastrowanego na indeks może być dodany tooother kolumn.  Jednak każdy indeks, która jest dodawana tabeli tooa doda miejsca i tooloads czasu przetwarzania.

toocreate tabeli indeks klastrowany, po prostu określić INDEKSU KLASTROWANEGO w klauzuli WITH hello:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd nieklastrowanego indeksu dla tabeli, po prostu hello użyj następującej składni:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Optymalizacja klastrowane indeksy magazynu kolumn
Tabel klastrowanego magazynu kolumn są zorganizowane w danych na segmenty.  Segment wysokiej jakości jest krytyczne tooachieving optymalnego działania zapytań dla magazynu kolumn tabeli.  Jakość segmentu można mierząc hello liczbę wierszy w grupie skompresowany wiersza.  Jakość segmentu jest optymalny, gdy istnieją co najmniej 100K wiersze na wiersz skompresowany grupy i uzyskania w wydajności, ponieważ hello liczba wierszy w wierszu grupy podejście 1 048 576 wierszy, które jest hello większości wiersze, które mogą zawierać grupę wierszy.

Tworzenie i używanie Hello poniżej widoku na powitania toocompute Twojego systemu średnia liczba wierszy przypadających na wiersz grupy i zidentyfikować indeksach magazynu kolumn nieoptymalnych klastra.  Hello ostatniej kolumny w tym widoku wygeneruje jako instrukcji SQL, które mogą być używane toorebuild Twojego indeksów.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Teraz, po utworzeniu widoku hello, uruchom to zapytanie tooidentify tabel z grupy wierszy jest mniejsza niż 100 KB wierszy.  Oczywiście można próg hello tooincrease 100 k Jeśli szukasz więcej jakości optymalne segmentu. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Po uruchomieniu kwerendy hello można rozpocząć toolook hello dane i analiza wyników. W następującej tabeli opisano, jakie toolook dla w analizy grupy wierszy.

| Kolumna | Jak toouse tych danych |
| --- | --- |
| [table_partition_count] |Tabela hello jest podzielona na partycje, może oczekiwać toosee wyższa liczba grupy Otwórz wierszy. Każdej partycji w dystrybucji hello może teoretycznie istnieje grupa Otwórz wiersz skojarzony z nim. Uwzględnić to analizy. Mała tabelę, która ma zostać podzielona na partycje można zoptymalizowana przez usunięcie hello partycjonowania całkowicie, ponieważ może to poprawić kompresji. |
| [row_count_total] |Całkowita liczba wierszy dla tabeli hello. Na przykład można użyć tej wartości procentowej toocalculate wartości wierszy w stanie hello skompresowane. |
| [row_count_per_distribution_MAX] |Jeśli wszystkie wiersze są równomiernie ta wartość będzie hello docelowy liczba wierszy w dystrybucji. Porównuje tę wartość z hello compressed_rowgroup_count. |
| [COMPRESSED_rowgroup_rows] |Całkowita liczba wierszy w formacie magazynu kolumn dla tabeli hello. |
| [COMPRESSED_rowgroup_rows_AVG] |Jeśli hello średnią liczbę wierszy jest znacznie mniejsza niż hello maksymalna liczba rzędów grupy wierszy, należy rozważyć użycie CTAS lub ALTER INDEX REBUILD toorecompress hello danych |
| [COMPRESSED_rowgroup_count] |Liczba grup wierszy w formacie magazynu kolumn. Jeśli ta liczba jest bardzo duże w tabeli toohello relacji jest wskaźnik brakuje hello gęstość magazynu kolumn. |
| [COMPRESSED_rowgroup_rows_DELETED] |Wiersze logicznie są usuwane z formatu magazynu kolumn. Jeśli liczba hello jest wysoka rozmiar tootable względny, należy rozważyć ponowne tworzenie partycji hello lub odbudowanie hello indeksu, ponieważ spowoduje to usunięcie ich fizycznie. |
| [COMPRESSED_rowgroup_rows_MIN] |Użyj to w połączeniu z hello średnia i maksymalna liczba kolumn toounderstand hello zakres wartości dla grupy wierszy hello w Twojego magazynu kolumn. Niski numer powyżej wartości progowej obciążenia hello (102400 na partycji wyrównane dystrybucji) sugeruje, że optymalizacji są dostępne w hello ładowanie danych |
| [COMPRESSED_rowgroup_rows_MAX] |Jak powyżej |
| [OPEN_rowgroup_count] |Otwórz wiersz grupy to normalne zachowanie. Czy jedną spodziewać jednej grupy Otwórz wiersz na tabeli dystrybucji (60). Nadmiernej liczby sugeruje ładowania w partycji danych. Sprawdź hello partycjonowania strategii toomake się, że dźwięku |
| [OPEN_rowgroup_rows] |Każda grupa wiersza może mieć 1 048 576 wierszy w nim co najwyżej. Użyj tej wartości toosee jak Pełna grupy wierszy Otwórz hello są obecnie |
| [OPEN_rowgroup_rows_MIN] |Otwieranie obszaru roboczego grupy oznaczać, że dane jest strumieniem ładowany do tabeli hello albo które hello poprzedniego obciążenia rozrzucone za pośrednictwem pozostałe wiersze w tej grupie wiersza. Użyj hello MIN, MAX, AVG toosee kolumn, jak dużo danych jest znajdowało się w grupach Otwórz wiersz. W przypadku małych tabel może to być 100% wszystkich danych hello! W takim przypadku ALTER INDEX REBUILD tooforce hello toocolumnstore danych. |
| [OPEN_rowgroup_rows_MAX] |Jak powyżej |
| [OPEN_rowgroup_rows_AVG] |Jak powyżej |
| [CLOSED_rowgroup_rows] |Spójrz na powitania zamknięte wiersza grupy wierszy w celu sprawdzenia związane z poprawnością. |
| [CLOSED_rowgroup_count] |Hello liczba grupy zamkniętego wierszy powinna być niska, jeśli dowolne są widoczne w ogóle. Grupy zamkniętego wierszy może być przekonwertowany toocompressed rowg roups przy użyciu hello ALTER INDEX... REORGANIZACJA polecenia. Jednak nie jest to zwykle wymagane. Zamknięte grupy to grupy wierszy toocolumnstore automatycznie przekonwertowane przez proces "przenoszenia krotki" hello w tle. |
| [CLOSED_rowgroup_rows_MIN] |Grupy wierszy zamkniętego powinny mieć współczynnik wypełnienia bardzo duże. Jeśli brakuje hello współczynnika wypełnienia grupy zamkniętego wiersza dalsza analiza hello magazynu kolumn jest wymagana. |
| [CLOSED_rowgroup_rows_MAX] |Jak powyżej |
| [CLOSED_rowgroup_rows_AVG] |Jak powyżej |
| [Rebuild_Index_SQL] |Indeks magazynu kolumn toorebuild SQL dla tabeli |

## <a name="causes-of-poor-columnstore-index-quality"></a>Przyczyny jakości indeksu magazynu kolumn niska
W razie znalezienia tabel z segmentu słabą jakość ma tooidentify hello główną przyczynę.  Poniżej przedstawiono niektóre typowe przyczyny quaility niską segmentu:

1. Wykorzystania pamięci, gdy indeks został skompilowany.
2. Duża liczba operacji DML
3. Mała lub ścieknie operacji obciążenia
4. Zbyt wiele partycji

Te czynniki mogą powodować toohave indeksu magazynu kolumn znacznie mniejszy niż hello optymalne 1 milion wierszy na grupę wierszy.  Może również spowodować wierszy toogo toohello delta wiersza grupy, zamiast grupy skompresowany wiersza. 

### <a name="memory-pressure-when-index-was-built"></a>Wykorzystania pamięci, gdy indeks został skompilowany.
Hello liczba wierszy przypadających na grupę skompresowany wierszy są bezpośrednio powiązane toohello szerokość wiersza hello i hello ilość pamięci dostępna tooprocess hello grupę wierszy.  Jeśli wiersze są zapisywane tabel toocolumnstore wykorzystanie pamięci, może to spowodować obniżenie jakości segmentu magazynu kolumn.  W związku z tym hello najlepszym rozwiązaniem jest toogive hello sesji, który zapisuje tooas dostępu do tabel indeksu magazynu kolumn tooyour dużej ilości pamięci, jak to możliwe.  Ponieważ istnieje zależność między pamięcią i współbieżności, hello wskazówki dotyczące hello prawo, pamięci, których alokacji jest zależna od danych hello w każdym wierszu tabeli hello ilość DWU przydzielone tooyour systemu i hello ilość współbieżności gniazd, należy zapewnić toohello sesji, który zapisuje dane tooyour tabeli.  Najlepszym rozwiązaniem zaleca się uruchomienie z xlargerc, jeśli używasz DW300 lub mniej largerc, jeśli korzystasz z DW400 tooDW600 i mediumrc Jeśli używasz DW1000 lub nowszym.

### <a name="high-volume-of-dml-operations"></a>Duża liczba operacji DML
Duża liczba operacji DML, które aktualizować i usuwać wiersze można wprowadzać nieefektywne podejście do hello magazynu kolumn. Dotyczy to zwłaszcza po zmodyfikowaniu większość hello wierszy hello grupy wierszy.

* Usuwanie wiersza z grupy wierszy skompresowany tylko logicznie oznacza hello wiersza jako usunięte. Hello wiersza pozostaje w grupie skompresowany wiersza hello, dopóki odbudowaniu hello partycji lub tabeli.
* Wstawienie wiersza dodaje hello wiersza tootooan wewnętrznego magazynu wierszy tabeli o nazwie grupy wierszy delta. Hello wstawiony wiersz nie jest toocolumnstore przekonwertowany, aż grupy wierszy delta hello jest zapełniony i jest oznaczone jako zamknięte. Grupy wierszy zostaną zamknięte po osiągnięcia maksymalnej pojemności hello 1 048 576 wierszy. 
* Aktualizacja wiersza w formacie magazynu kolumn jest przetwarzany jako delete logicznej, a następnie insert. Wiersz wstawiony Hello mogą być przechowywane w magazynie delta hello.

Umieścić w zadaniu wsadowym aktualizacji i Wstaw operacje przekraczające próg zbiorczego hello 102 400 wierszy przypadających na partycję wyrównany dystrybucji będą zapisywane bezpośrednio formatu toohello magazynu kolumn. Jednak przy założeniu Rozdziel, będzie potrzebny toobe modyfikowanie więcej niż 6.144 mln wierszy w ramach jednej operacji dla tego toooccur. Jeśli hello liczbę wierszy dla danej partycji wyrównane dystrybucji znajduje się mniej niż 102400 wierszy hello przejdzie toohello delta magazynu i pozostaną dostępne do momentu wystarczające wiersze zostały wstawione lub zmodyfikowane tooclose hello grupy lub hello indeks wiersza został ponownie skompilowany.

### <a name="small-or-trickle-load-operations"></a>Mała lub ścieknie operacji obciążenia
Mała liczba godzin ładuje, że przepływ do usługi SQL Data Warehouse czasami nazywa się ścieknie obciążeń. Zazwyczaj reprezentują near stały strumień danych jest pozyskanych przez hello system. Jednak ponieważ ten strumień jest bliski ciągłego hello wolumin wierszy nie jest szczególnie duże. Najczęściej danych hello jest znacznie poniżej wartości progowej hello wymagane dla formatu toocolumnstore ładowania bezpośredniego.

W takich przypadkach często jest lepsze danych hello tooland najpierw w magazynie obiektów blob platformy Azure i pozwól mu gromadzone tooloading wcześniejszych. Ta metoda jest często nazywany *przetwarzanie wsadowe micro*.

### <a name="too-many-partitions"></a>Zbyt wiele partycji
Inny element tooconsider jest wpływ hello partycjonowania na tabel klastrowanego magazynu kolumn.  Przed partycje, SQL Data Warehouse już dzieli dane 60 baz danych.  Dodatkowo partycjonowania dzieli dane.  Jeśli partycji danych, a następnie można tooconsider który **każdego** partycji będzie potrzebne toohave co najmniej 1 milion wierszy toobenefit z klastrowanego indeksu magazynu kolumn.  Jeśli partycji tabeli na partycje 100, a następnie tabeli należy toohave co najmniej 6 miliard wierszy toobenefit z klastrowanego indeksu magazynu kolumn (60 dystrybucje * partycje 100 * 1 milion wierszy). Jeśli 100 partycji tabeli nie ma 6 miliardy wierszy, Zmniejsz liczbę hello partycji lub tabeli sterty zamiast tego Rozważ użycie.

Po tabele zostały załadowane z niektórych danych, wykonaj hello poniżej tooidentify kroki i Przebuduj tabele z indeksami magazynu kolumn nieoptymalnych klastra.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Ponowne tworzenie indeksów tooimprove segmentu jakości
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Krok 1: Określenie lub Utwórz użytkownika, który używa klasy zasobu prawo hello
Jednym ze sposobów szybkiego tooimmediately poprawić jakość segmentu jest toorebuild hello indeksu.  Hello zwrócony przez hello powyżej widoku SQL zwróci instrukcji ALTER INDEX REBUILD, które mogą być używane toorebuild Twojego indeksów.  Ponowne tworzenie indeksów sieci, należy pamiętać, że przydzielić wystarczającej ilości pamięci sesji toohello, który będzie odbudowanie indeksu.  toodo tej, Zwiększ hello zasobów klasy użytkownika, który ma uprawnienia toorebuild hello indeks minimalna zalecana toohello tabeli.  Nie można zmienić klasy zasobów Hello użytkownika właściciela bazy danych hello, więc jeśli nie utworzono użytkownika w systemie hello, konieczne będzie toodo najpierw.  zalecanym przez nas minimum Hello jest xlargerc Jeśli używasz DW300 lub mniej, largerc Jeśli korzystasz z DW400 tooDW600 i mediumrc Jeśli używasz DW1000 lub nowszym.

Poniżej znajduje się przykład sposobu tooallocate więcej pamięci tooa użytkownika przez odpowiednie zwiększenie ich klasy zasobów.  Aby uzyskać więcej informacji na temat klasy zasobów i jak toocreate nowego użytkownika można znaleźć w hello [zarządzania współbieżności i obciążenia] [ Concurrency] artykułu.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Krok 2: Ponownie klastrowane indeksy magazynu kolumn za pomocą nowszej użytkownika klasy zasobu
Zaloguj się jako hello użytkownika z kroku 1 (np. LoadUser), który jest teraz za pomocą nowszej klasy zasobów i wykonywania instrukcji ALTER INDEX hello.  Pamiętaj, że ten użytkownik ma toohello tabel uprawnienie ALTER, gdzie jest odbudować indeksu hello.  Poniższe przykłady pokazują, jak toorebuild hello indeksu magazynu kolumn całą lub jak toorebuild jednej partycji. W dużych tabel jest bardziej praktyczne indeksów toorebuild pojedynczej partycji naraz.

Możesz też zamiast odbudowanie indeksu hello, można skopiować hello tabeli tooa nowej tabeli za pomocą [CTAS][CTAS].  Jaki sposób jest najlepsza? Dla dużych ilości danych [CTAS] [ CTAS] jest zwykle szybsze niż [ALTER INDEX][ALTER INDEX]. W przypadku mniejszych woluminów danych [ALTER INDEX] [ ALTER INDEX] jest łatwiejsze toouse i nie wymaga tooswap limit hello tabeli.  Zobacz **ponowne tworzenie indeksów CTAS i przełączanie partycji** poniżej uzyskać więcej informacji dotyczących sposobu toorebuild indeksy z CTAS.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

Ponowne tworzenie indeksu w usłudze SQL Data Warehouse jest operacją w trybie offline.  Aby uzyskać więcej informacji na temat ponowne tworzenie indeksów, zobacz hello polecenia ALTER INDEX REBUILD sekcji [defragmentacji indeksy magazynu kolumn] [ Columnstore Indexes Defragmentation] i tematu składni hello [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Krok 3: Sprawdź, czy uległa poprawie jakości segmentu klastrowanego magazynu kolumn
Uruchom ponownie hello zapytania, którego tabeli z słaby segment jakości i sprawdź, czy uległa poprawie jakości segmentu.  Jeśli nie poprawy jakości segmentu, może to być czy hello wierszy w tabeli są bardzo szeroki.  Należy rozważyć użycie nowszej klasy zasobu lub DWU podczas odbudowywania z indeksów.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Ponowne tworzenie indeksów CTAS i przełączanie partycji
W tym przykładzie użyto [CTAS] [ CTAS] i przełączania toorebuild partycji tabeli partycji. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Aby uzyskać więcej informacji o ponowne tworzenie partycji przy użyciu `CTAS`, zobacz hello [partycji] [ Partition] artykułu.

## <a name="next-steps"></a>Następne kroki
toolearn więcej, zobacz artykuły hello na [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Partycjonowania tabeli][Partition], [utrzymania statystyk tabeli] [ Statistics] i [ Tabele tymczasowe][Temporary].  toolearn więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
