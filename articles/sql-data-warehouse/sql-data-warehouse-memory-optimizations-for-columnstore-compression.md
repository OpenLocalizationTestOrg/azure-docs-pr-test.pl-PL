---
title: "wydajność indeksu magazynu kolumn aaaImprove SQL Azure | Dokumentacja firmy Microsoft"
description: "Zmniejsz wymagania dotyczące pamięci lub zwiększ hello dostępnej pamięci toomaximize hello liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Maksymalizacja jakości i dla magazynu kolumn

Jakość i jest określana przez hello liczbę wierszy w grupy wierszy. Zmniejsz wymagania dotyczące pamięci lub zwiększ hello dostępnej pamięci toomaximize hello liczbę wierszy indeksu magazynu kolumn kompresuje do każdej grupy wierszy.  Użyj tych metody tooimprove kompresji szybkości i wydajności zapytań dla indeksów magazynu kolumn.

## <a name="why-hello-rowgroup-size-matters"></a>Dlaczego hello i rozmiar ma znaczenie
Ponieważ indeks magazynu kolumn skanowania tabeli za pomocą skanowania segmentów kolumny z poszczególnych rowgroups, maksymalizacja hello liczbę wierszy w każdym i zwiększa wydajność zapytań. Gdy rowgroups ma dużą liczbę wierszy, kompresji danych zwiększa, co oznacza, że istnieje mniej tooread danych z dysku.

Aby uzyskać więcej informacji o rowgroups, zobacz [przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Rozmiar docelowy rowgroups
Aby uzyskać najlepszą wydajność zapytań celem hello jest toomaximize hello liczba wierszy przypadających na grupy wierszy w indeksie magazynu kolumn. I może mieć maksymalnie 1 048 576 wierszy. Jego zgadzasz toonot ma hello maksymalna liczba wierszy przypadających na grupy wierszy. Indeksy magazynu kolumn uzyskać dobrą wydajność, gdy rowgroups zawiera co najmniej 100 000 wierszy.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Rowgroups można pobrać usuwane podczas kompresji

Podczas zbiorczego obciążenia lub magazynu kolumn odbudowywanie indeksu czasami nie ma wystarczającej ilości pamięci dostępnej toocompress hello wszystkie wiersze przeznaczone dla każdej grupy wierszy. W przypadku wykorzystania pamięci indeksy magazynu kolumn trim hello rozmiary i dlatego może się powieść kompresji w hello magazynu kolumn. 

Usługi SQL Data Warehouse generuje błąd, w przypadku niewystarczającej ilości pamięci toocompress co najmniej 10 000 wierszy do każdej grupy wierszy.

Aby uzyskać więcej informacji dotyczących ładowania zbiorczego, zobacz [ładowanie zbiorcze do klastrowanego indeksu magazynu kolumn](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Jak toomonitor i jakość

Brak udostępnia przydatne informacje, takie jak liczba wierszy w rowgroups i hello Przyczyna przycinanie, jeśli został przycinanie DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats). Te informacje tooget DMV hello następującego widoku w postaci tooquery wygodny sposób można tworzyć na przycinanie grupy wierszy.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hello trim_reason_desc informuje, czy został przycięty i hello (trim_reason_desc = NO_TRIM oznacza nie było żadnych przycinanie i grupę wierszy jest jakość). Witaj skutkiem przycinania oznaczać przedwczesny przycinanie i hello:
- BULKLOAD: Z tego powodu przycinania jest używany podczas hello przychodzące partii wierszy dla obciążenia hello ma mniej niż 1 milion wierszy. Jeśli jest większa niż 100 000 wierszy wstawiane (w przeciwieństwie tooinserting do magazynu delta hello), ale zestawy hello tooBULKLOAD przycinania Przyczyna aparat Hello utworzy grupy wierszy skompresowane. W tym scenariuszu należy rozważyć zwiększenie tooaccumulate okna obciążenia sieci partii więcej wierszy. Ponadto obliczyć ponownie Twoje partycjonowania tooensure schematu nie jest zbyt szczegółowego jako grupy wierszy nie może obejmować granice partycji.
- MEMORY_LIMITATION: toocreate grupy wiersza o 1 milion wierszy, określoną ilość pamięci roboczej jest wymagana przez aparat hello. Gdy dostępna pamięć hello ładowania sesji jest mniejszy niż wymagane hello pracy pamięci, grupy wierszy przedwcześnie uzyskać usuwane. następujące sekcje Hello Wyjaśnij, jak tooestimate pamięci wymagane i przydzielenie większej ilości pamięci.
- DICTIONARY_SIZE: Z tego powodu przycinania wskazuje, że przycinanie i wystąpił, ponieważ wystąpił co najmniej jednej kolumny typu string z ciągami Kardynalność szerokości i/lub wysokiego. Rozmiar słownika Hello jest ograniczona too16, który jest skompresowany MB w pamięci i po osiągnięciu tego limitu hello grupę wierszy. Jeśli zostanie uruchomione w tej sytuacji, należy wziąć pod uwagę izolowanie hello kolumny powodować problemy w osobnej tabeli.

## <a name="how-tooestimate-memory-requirements"></a>Jak tooestimate wymagania dotyczące pamięci

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Witaj maksymalna ilość pamięci wymagana toocompress jednej grupy wierszy wynosi około

- 72 MB +
- \#wiersze \* \#kolumn \* 8 bajtów +
- \#wiersze \* \#krótki ciąg kolumn \* 32 bajtów +
- \#długi ciąg kolumn \* 16 MB dla słownika kompresji

gdzie krótki ciąg kolumn używać typów danych ciąg < = 32 bajtów i użyj długi ciąg kolumn danych typu ciąg > 32 bajtów.

Długie ciągi są kompresowane za pomocą metody kompresji przeznaczone do kompresowania tekstu. Ta metoda kompresji używa *słownika* toostore wzorce tekstu. Maksymalny rozmiar słownika Hello jest 16 MB. Istnieje tylko jeden słownika dla każdej kolumny długi ciąg hello grupy wierszy.

Szczegółowe omówienie wymagań pamięci magazynu kolumn, zobacz wideo [skalowania usługi Azure SQL Data Warehouse: wskazówki i konfiguracji](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Wymagania dotyczące sposobów tooreduce pamięci

Użyj hello następujące techniki tooreduce hello wymagania dotyczące pamięci kompresowania rowgroups w indeksach magazynu kolumn.

### <a name="use-fewer-columns"></a>Użyj mniejszej liczby kolumn
Jeśli to możliwe projektowanie hello tabeli z mniejszą liczbą kolumn. Podczas kompresji i do magazynu kolumn hello indeksu magazynu kolumn hello oddzielnie kompresuje każdego segmentu kolumny. Witaj w związku z tym wymagania dotyczące pamięci, które toocompress i zwiększyć jako hello liczba wzrasta kolumn.


### <a name="use-fewer-string-columns"></a>Użyj mniejszej liczby kolumn ciągu
Kolumny danych typu ciąg wymaga więcej pamięci niż liczbowych i typy danych Data. tooreduce wymagania dotyczące pamięci, rozważ usunięcie kolumny ciągu z tabel faktów i umieszczania ich w mniejszych tabele wymiarów.

Wymagania dotyczące pamięci dodatkowe ciąg kompresji:

- Typy danych parametry się znaki too32 może wymagać 32 bajtów dodatkowe na wartość.
- Typy danych ciąg z więcej niż 32 znaki są kompresowane przy użyciu metod słownika.  Każda kolumna hello i może wymagać się tooan dodatkowe 16 MB toobuild hello słownika.

### <a name="avoid-over-partitioning"></a>Unikaj nadmiernego partycjonowania

Indeksy magazynu kolumn utworzyć rowgroups co najmniej jednej partycji. W usłudze SQL Data Warehouse hello liczby partycji rozwoju szybko ponieważ hello dane są przesyłane i każdej dystrybucji jest podzielona na partycje. Jeśli tabela hello ma zbyt wiele partycji, może nie być wystarczającej ilości rowgroups hello toofill wierszy. Brak Hello wierszy nie tworzy wykorzystania pamięci podczas kompresji, ale prowadzi toorowgroups, który nie będzie hello najlepszą wydajność zapytań magazynu kolumn.

Inny Przyczyna tooavoid nadmiernie Partycjonowanie jest pamięci w czasie ładowania wierszy do indeksu magazynu kolumn dla partycjonowanej tabeli. Podczas ładowania większej liczby partycji można odebrać hello przychodzących wierszy, które są przechowywane w pamięci, dopóki każda partycja ma za mało toobe wierszy skompresowane. Zbyt wiele partycji mających tworzy wykorzystania pamięci dodatkowe.

### <a name="simplify-hello-load-query"></a>Uproszczenie hello obciążenia zapytania

Witaj bazy danych udziałów hello przydział pamięci dla zapytania wśród wszystkich operatorów hello w zapytaniu hello. Jeśli zapytanie obciążenia sortowania złożonego i sprzężeń, zostanie zmniejszona pamięci hello kompresji.

Projektowanie hello obciążenia zapytania toofocus tylko na ładowanie hello zapytania. Przekształcenia toorun na powitania danych, należy uruchomić je oddzielnie od hello obciążenia zapytania. Na przykład etap hello dane w tabeli sterty, uruchom przekształcenia hello, a następnie załadować hello Tabela przemieszczania do hello indeksu magazynu kolumn. Można również najpierw załadować dane hello, a następnie użyć hello MPP systemu tootransform hello danych.

### <a name="adjust-maxdop"></a>Dostosuj MAXDOP

Każdy dystrybucji kompresuje rowgroups do magazynu kolumn hello równoległe, gdy jest dostępna więcej niż jednego rdzenia procesora CPU na dystrybucji. Równoległość Hello wymaga dodatkowych zasobów pamięci, które mogą prowadzić toomemory wykorzystania i przycinanie i.

tooreduce wykorzystania pamięci, można użyć hello MAXDOP zapytania wskazówka tooforce hello obciążenia operacji toorun w trybie serial w ramach poszczególnych dystrybucji.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Sposoby tooallocate większej ilości pamięci

DWU rozmiaru i hello zasobów klasy użytkownika ze sobą określić ilość pamięci dostępnej dla zapytania użytkownika. tooincrease hello pamięci przyznać dla zapytania obciążenia, możesz zwiększyć hello liczby jednostek dwu lub zwiększyć hello klasy zasobów.

- Witaj tooincrease jednostek dwu, zobacz [sposób skalowania wydajności?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- Klasa zasobów hello toochange dla zapytania, zobacz [zmienić przykład klasy zasobów użytkownika](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Na przykład na DWU 100 użytkownika w klasie zasobu smallrc hello służy 100 MB pamięci dla poszczególnych dystrybucji. Aby hello uzyskać szczegółowe informacje, zobacz [współbieżność w usłudze SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Załóżmy, że należy określić, czy potrzebujesz 700 MB pamięci tooget wysokiej jakości i rozmiary. Poniższe przykłady pokazują, jak można uruchomić zapytania obciążenia hello o wystarczającej ilości pamięci.

- Korzystając z DWU 1000 i mediumrc, Twoje przydział pamięci jest 800 MB
- Korzystając z DWU 600 i largerc, Twoje przydział pamięci jest 800 MB.


## <a name="next-steps"></a>Następne kroki

toofind więcej sposobów tooimprove wydajności w usłudze SQL Data Warehouse, zobacz hello [wydajności — omówienie](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
