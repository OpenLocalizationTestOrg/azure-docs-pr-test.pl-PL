---
title: "aaaDesign wskazówki dotyczące zreplikowane tabele - Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówek dotyczących projektowania zreplikowane tabele w schemat magazyn danych SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Wskazówki dotyczące projektowania dotyczące używania zreplikowane tabele w magazynie danych SQL Azure
Ten artykuł zawiera zalecenia dotyczące projektowania zreplikowanych tabel w schematu SQL Data Warehouse. Aby użyć wydajność zapytań tooimprove te zalecenia zmniejsza się złożoność danych przemieszczania i zapytań.

> [!NOTE]
> Funkcja zreplikowanej tabeli Hello jest obecnie w wersji zapoznawczej. Niektóre zachowania są toochange podmiotu.
> 

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że znasz z danych dystrybucji i koncepcje przepływu danych w usłudze SQL Data Warehouse.  Aby uzyskać więcej informacji, zobacz [rozproszonych danych](sql-data-warehouse-distributed-data.md). 

W ramach projektowaniu tabel Dowiedz się, jak to możliwe danych i jak danych hello jest poddawany kwerendzie.  Na przykład wziąć pod uwagę następujące pytania:

- Jak duże jest tabela hello?   
- Częstotliwość odświeżania tabeli hello?   
- Tabele faktów i wymiarów są dostępne w magazynie danych?   

## <a name="what-is-a-replicated-table"></a>Co to jest zreplikowanej tabeli?
Zreplikowanej tabeli ma pełną kopię tabeli hello jest dostępny w każdym węźle obliczeń. Replikowanie tabeli usuwa hello potrzeby tootransfer danych między węzłami obliczeniowymi przed join lub agregacji. Ponieważ hello tabela ma wiele kopii, zreplikowanych tabelach działają najlepiej, gdy rozmiar tabeli hello jest mniejszy niż 2 GB skompresowane.

Witaj Poniższy diagram przedstawia zreplikowanej tabeli, która jest dostępna w każdym węźle obliczeń. W usłudze SQL Data Warehouse zreplikowanej tabeli hello jest bazy danych dystrybucji tooa całkowicie skopiowane na każdym węźle obliczeniowym. 

![Tabela zreplikowane](media/guidance-for-using-replicated-tables/replicated-table.png "zreplikowane tabeli")  

Replikowane tabele pracy efektywne w przypadku tabel wymiarów małych w schemat gwiazdy. Tabele wymiarów zwykle mają rozmiar, dzięki którym możliwe toostore i obsługa wielu kopii. Wymiary przechowywać opisowe dane, które zmienia się powoli, takie jak nazwa klienta i adresem i szczegółowe informacje. Hello powoli zmiana rodzaju danych hello prowadzi toofewer odbudowuje hello zreplikowanej tabeli. 

Należy rozważyć użycie zreplikowanej tabeli, gdy:

- rozmiar tabeli Hello na dysku jest mniejszy niż 2 GB, niezależnie od hello liczbę wierszy. rozmiar hello toofind tabeli, można użyć hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) polecenia: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- Tabela Hello jest używana w sprzężeniu, które w przeciwnym razie wymaga przenoszenia danych. Na przykład sprzężenia w tabelach rozpowszechniane skrót wymaga przenoszenia danych, gdy hello łącząca kolumn nie są hello tej samej kolumnie dystrybucji. Jedną z tabel rozpowszechniane skrót hello jest mały, należy wziąć pod uwagę zreplikowanej tabeli. Sprzężenia w tabeli okrężnego wymaga przenoszenia danych. Zalecamy używanie zamiast okrężnego tabel w większości przypadków zreplikowanych tabelach. 


Należy wziąć pod uwagę Konwertowanie istniejącej rozproszonej tooa tabeli replikowane tabeli, gdy:

- Zapytanie plany operacje przenoszenia danych użycia, które emisji węzły obliczeniowe hello tooall danych hello. Hello BroadcastMoveOperation jest kosztowne i zmniejsza wydajność kwerend. Użyj tooview operacje przenoszenia danych w planie zapytania [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Zreplikowane tabele nie mogą użyć instrukcji yield hello najlepszą wydajność zapytań po:

- Tabela Hello ma częste wstawiania, aktualizowania i usuwania działań. Te operacje języka manipulacji danych wymaga odbudowania hello replikowane tabeli. Ponowne kompilowanie często powodują mniejszą wydajność.
- Magazyn danych Hello jest skalowana często. Skalowanie hurtowni danych zmienia hello liczbę węzłów obliczeniowych, co wiąże się z odbudowie.
- Tabela Hello ma dużą liczbę kolumn, ale operacje na danych zwykle uzyskują dostęp do niewielkiej liczby kolumn. W tym scenariuszu, zamiast replikować całą tabelę hello, może być toohash bardziej efektywnej dystrybucji hello tabeli, a następnie utworzyć indeks kolumny hello często używane. Gdy zapytanie wymaga przenoszenia danych, Magazyn danych SQL tylko przenosi dane w hello żądanej kolumny. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Zreplikowane tabele za pomocą prostego zapytania predykatów
Przed wybierz toodistribute lub replikacji tabeli, należy zastanowić hello typy zapytań, które mają toorun hello tabeli. Jeśli to możliwe,

- Użyj zreplikowanych tabel dla zapytań z predykaty prostego zapytania, takie jak równości i nierówności.
- Użyj tabel rozproszone dla zapytań z predykaty złożonego zapytania, takie jak podobne lub nie, takich jak.

Użycie Procesora CPU zapytania wykonywane najlepiej, jeśli praca hello jest dystrybuowana do wszystkich węzłów obliczeniowych hello. Na przykład zapytania uruchamiane obliczenia w każdym wierszu tabeli działać lepiej w tabelach rozproszonej niż zreplikowanych tabelach. Ponieważ zreplikowanej tabeli są przechowywane w całości w każdym węźle obliczeń, użycie Procesora CPU zapytanie zreplikowanej tabeli jest uruchamiana dla całej tabeli hello w każdym węźle obliczeń. Hello dodatkowe obliczeń może zmniejszyć wydajność wykonywania zapytań.

Na przykład ta kwerenda zawiera złożone predykatu.  Uruchamia szybciej gdy dostawca jest tabela rozproszona zamiast zreplikowanej tabeli. W tym przykładzie dostawcy mogą być dystrybuowane wyznaczania wartości skrótu, albo rozproszone okrężnego.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Konwertowanie istniejących tabel tooreplicated tabel okrężnego
Jeśli masz już okrężnego tabel, zaleca się ich konwertowania tooreplicated tabel, gdy spełniają kryteria opisane w tym artykule. Zreplikowane tabele zwiększyć wydajność w przypadku tabel okrężnego, ponieważ eliminuje konieczność hello przenoszenia danych.  Tabela okrężnego zawsze wymaga przenoszenia danych sprzężenia. 

W tym przykładzie użyto [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tabeli tooa replikowane tabeli. W tym przykładzie działa niezależnie od tego, czy DimSalesTerritory rozpowszechniane skrót lub okrężnego.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Przykład wydajności kwerendy okrężnego i replikowane 

Zreplikowanej tabeli nie wymaga przenoszenia żadnych danych dla sprzężeń, ponieważ hello cała tabela jest już obecny w każdym węźle obliczeń. Jeśli tabele wymiarów hello okrężnego rozproszonych, sprzężenia kopiuje hello tabeli wymiarów w węźle obliczeń tooeach pełna. dane hello toomove, hello planu zapytania zawiera operacji o nazwie BroadcastMoveOperation. Ten typ operacji przenoszenia danych zmniejsza wydajność zapytań i wyeliminowania przy użyciu zreplikowanych tabelach. tooview kroki planu zapytania, użyj hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) widoku wykazu systemu. 

Na przykład, w następującej kwerendy względem schematu AdventureWorks hello hello ` FactInternetSales` tabela jest dystrybuowane wyznaczania wartości skrótu. Witaj `DimDate` i `DimSalesTerritory` tabele są mniejsze tabele wymiarów. Ta kwerenda zwraca hello sprzedaży w Ameryce Północnej, dla roku obrachunkowego 2004:
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Ponownie utworzono `DimDate` i `DimSalesTerritory` jako tabele okrężnego. W związku z tym hello zapytania wykazało hello planu zapytania, który ma wiele emisji operacje są przenoszone z następujących: 
 
![Plan zapytania okrężnego](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Ponownie utworzono `DimDate` i `DimSalesTerritory` jako zreplikowane tabele i ponownie uruchomiono hello zapytania. Wynikowa planu zapytania Hello jest znacznie krótszy i nie ma żadnego emituje przenosi.

![Replikowane planu zapytania](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Zagadnienia dotyczące wydajności modyfikowania zreplikowanych tabelach
Usługa SQL Data Warehouse implementuje zreplikowanej tabeli dzięki utrzymywaniu głównej wersji hello tabeli. Kopiuje bazy danych dystrybucji tooone głównej wersji hello w każdym węźle obliczeń. W przypadku zmiany SQL Data Warehouse najpierw aktualizuje hello wzorcowej tabeli. Następnie wymaga odbudowania hello tabel w każdym węźle obliczeń. Kompilowania zreplikowanej tabeli obejmuje kopiowanie węzeł obliczeniowy tooeach hello w tabeli, a następnie odbudowanie hello indeksów.

Odtwarza są wymagane po:
- Dane są ładowane lub zmodyfikowane
- Hello data warehouse jest skalowaną tooa różnych wartości DWU ustawienia
- Definicja tabeli jest aktualizowany

Odtwarza nie są wymagane po:
- Operację wstrzymywania
- Wznawia działania

Odbuduj Hello nie odbywa się natychmiast po zmodyfikowaniu danych. Zamiast tego wyzwoleniu odbudowy hello hello wybiera zapytania z tabeli powitania po raz pierwszy.  W ramach początkowego instrukcji select hello z tabeli hello są kroki toorebuild hello zreplikowanej tabeli.  Ponieważ Odbuduj hello jest wykonywana w ramach zapytania hello, początkowego instrukcji select hello wpływ toohello może być istotne w zależności od wielkości hello hello tabeli.  Jeśli wiele zreplikowanych tabelach są zaangażowane wymagające kompilowania, każda kopia zostanie odtworzony pojedynczo jako kroków w ramach instrukcji hello.  spójność danych toomaintain podczas kompilowania hello hello replikowane wyłącznej blokady jest wykonywana na tabeli hello tabeli.  Blokada Hello zapobiega wszystkich tabeli toohello dostępu na czas trwania hello hello odbudowy. 

### <a name="use-indexes-conservatively"></a>Użyj konserwatywnie indeksów
Rozwiązania w zakresie indeksowania standardowe mają zastosowanie tooreplicated tabel. Usługi SQL Data Warehouse odbudowuje każdy indeks zreplikowanej tabeli jako część hello ponownej kompilacji. Indeksy należy używać tylko w przypadku bardziej wydajne hello podejścia są większe niż koszty hello ponowne tworzenie indeksów hello.  
 
### <a name="batch-data-loads"></a>Ilości danych w partii
Podczas ładowania danych w zreplikowanych tabelach, spróbuj odtwarza toominimize razem przetwarzanie wsadowe obciążeń. Wykonaj wszystkie obciążenia hello umieścić w zadaniu wsadowym przed uruchomieniem instrukcji "select".

Na przykład tego wzorca obciążenia ładuje dane z czterech źródeł i wywołuje cztery odtwarza. 

- Załaduj ze źródła 1.
- Instrukcja SELECT wyzwalaczy odbudować 1.
- Załaduj ze źródła 2.
- Instrukcja SELECT wyzwalaczy odbudować 2.
- Załaduj ze źródła 3.
- Instrukcja SELECT wyzwalaczy odbudować 3.
- Załaduj ze źródła 4.
- Instrukcja SELECT wyzwalaczy odbudować 4.

Na przykład tego wzorca obciążenia ładuje z czterech źródeł danych, ale tylko wywołuje jeden ponownej kompilacji.

- Załaduj ze źródła 1.
- Załaduj ze źródła 2.
- Załaduj ze źródła 3.
- Załaduj ze źródła 4.
- Odbuduj wyzwalaczy instrukcji SELECT.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Odbuduj zreplikowanej tabeli po załadowaniu partii
czas wykonywania zapytania spójne tooensure, zaleca się wymuszanie odświeżania tabel hello replikowane po załadowaniu partii. W przeciwnym razie hello pierwszego zapytania należy poczekać hello toorefresh tabel, która obejmuje ponowne tworzenie indeksów hello. W zależności od rozmiaru hello i liczby zreplikowanych tabel, których to dotyczy hello wpływ na wydajność może być istotne.  

To zapytanie używa hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello zreplikowane tabele, które zostały zmodyfikowane, ale nie został odbudowany.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce kompilowania, uruchom powitania po instrukcji w każdej tabeli w hello poprzedzających danych wyjściowych. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Następne kroki 
toocreate zreplikowanej tabeli, użyj jednej z tych instrukcji:

- [Utwórz tabelę (magazyn danych Azure SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [Utwórz TABLE AS SELECT (magazyn danych Azure SQL](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Omówienie rozproszonej tabel, zobacz [rozproszonych tabel](sql-data-warehouse-tables-distribute.md).



