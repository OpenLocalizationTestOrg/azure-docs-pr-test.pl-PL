---
title: "Klasy zasobów dla obciążenia zarządzania - Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące zarządzania współbieżności i obliczeniowe zasobów dla zapytań w usłudze Azure SQL Data Warehouse przy użyciu klasy zasobów."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 122646f73b6e4e7c62eb0e6d4b6672b603d8acb2
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/25/2017
---
# <a name="resource-classes-for-workload-management"></a>Klasy zasobów do zarządzania obciążenia
Wskazówki dotyczące liczby równoczesnych zapytań, uruchamiać jednocześnie, które zasoby zapytań w usłudze Azure SQL Data Warehouse obliczeniowe zarządzanie za pomocą klasy zasobów.
 
## <a name="what-is-workload-management"></a>Co to jest zarządzanie obciążenie?
Zarządzanie obciążenie jest możliwość optymalizacji ogólną wydajność wszystkich zapytań. Dobrze Zaczekaj obciążenie działa zapytań i operacji obciążenia wydajnie niezależnie od tego, czy są one obliczeniowych lub intensywnie wykonujących operacje We/Wy. 

Usługa SQL Data Warehouse zapewnia funkcje zarządzania obciążenia w środowiskach wielu użytkowników. Magazyn danych nie jest przeznaczony dla wielu dzierżawców obciążeń.

## <a name="what-are-resource-classes"></a>Co to są klasy zasobu?
Klasy zasobów są limity wstępnie określonych zasobów, które określają sposób wykonywania zapytania. Usługa SQL Data Warehouse ogranicza zasoby obliczeniowe dla każdego zapytania według klasy zasobów. 

Zasób klas ułatwia zarządzanie usługą ogólną wydajność obciążenia magazynu danych. Efektywne korzystanie z zasobów klas pomaga w zarządzaniu obciążenie przez ustawienie limitów liczby zapytania uruchamiane jednocześnie oraz zasoby obliczeniowe przypisane do każdego zapytania. 

- Mniejsze klasy zasobu zużywać mniej zasobów obliczeniowych, ale włączyć większa ogólną współbieżności zapytania
- Większe grupy zasobów zapewniają więcej zasoby obliczeniowe, ale ograniczyć współbieżności zapytania

Klasy zasobów są przeznaczone dla działania zarządzania i manipulowania nimi danych. Niektóre bardzo złożonych zapytań będzie również skorzystać w przypadku dużych sprzężenia i sortowanie, aby system wykonuje zapytania w pamięci, a nie przechodzeniu na dysku.

Klasy zasobów zależą następujące operacje:

* WYBIERZ OPCJĘ INSERT, UPDATE, DELETE
* Wybierz (podczas wykonywania zapytania tabele użytkownika)
* ALTER INDEX - ODBUDOWY lub ZREORGANIZOWAĆ
* ALTER TABLE REBUILD
* TWORZENIE INDEKSU
* UTWÓRZ KLASTROWANY INDEKS MAGAZYNU KOLUMN
* UTWÓRZ TABLE AS SELECT (CTAS)
* Ładowanie danych
* Operacje przenoszenia danych prowadzone przez usługi przenoszenia danych (DMS)

> [!NOTE]  
> Wybierz instrukcje na dynamicznych widoków zarządzania (widoków DMV) lub innych system, który nie podlegają widoków przy użyciu jednej z limitami współbieżności. Można monitorować system niezależnie od liczby zapytań wykonywanych na nim.
> 
> 

## <a name="static-and-dynamic-resource-classes"></a>Klas statycznych i dynamicznych zasobów

Istnieją dwa typy klasy zasobu: dynamiczną i statyczną.

- **Klasy statyczne zasobów** przydzielić tego samego ilość pamięci, niezależnie od bieżącego poziomu usługi, która jest mierzona w [jednostki magazynu danych](what-is-a-data-warehouse-unit-dwu-cdwu.md). Ten przydział statycznych oznacza na większych poziomów usług można uruchomić zapytania więcej w każdej klasy zasobów.  Klasy statyczne zasobów są nazywane staticrc10, staticrc20 staticrc30, staticrc40, staticrc50, staticrc60, staticrc70 i staticrc80. Te klasy zasobów są najlepiej nadaje się do rozwiązania, które zwiększają klasy zasobów, aby uzyskać dodatkowe zasoby obliczeniowe zasobów.

- **Dynamiczne klasy zasobu** przydzielić zmiennej ilość pamięci w zależności od bieżącego poziomu usługi. Skalowanie w górę na większy poziom usługi, kwerend automatycznie Pobierz więcej pamięci. Klasy zasobu dynamicznego są nazywane smallrc, mediumrc largerc i xlargerc. Te klasy zasobów są najbardziej odpowiednie do skalowania, aby uzyskać dodatkowe zasoby obliczeniowe które wzrost rozwiązań. 

[Warstwy wydajności](performance-tiers.md) używać tych samych nazw klasy zasobów, ale mają różne [pamięci i specyfikacje](performance-tiers.md). 


## <a name="assigning-resource-classes"></a>Przypisywanie klasy zasobu

Klasy zasobów są implementowane przez przypisywania użytkowników do ról bazy danych. Gdy użytkownik uruchamia kwerendy, kwerenda działa klasy zasobów użytkownika. Na przykład jeśli użytkownik jest członkiem roli bazy danych smallrc lub staticrc10, ich zapytania uruchamiane z małej ilości pamięci. Gdy użytkownik bazy danych jest elementem członkowskim xlargerc lub staticrc80 ról bazy danych, ich zapytania uruchamiane z dużą ilością pamięci. 

Aby zwiększyć klasy zasobów użytkownika, użyj procedury składowanej [sp_addrolemember](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql). 

```sql
EXEC sp_addrolemember 'largerc', 'loaduser';
```

Aby zmniejszyć klasy zasobów, użyj [sp_droprolemember](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql).  

```sql
EXEC sp_droprolemember 'largerc', 'loaduser';
```

Klasa zasobu administratora usługi jest stała i nie można zmienić.  Administrator usługi jest użytkownika utworzonym podczas procesu inicjowania obsługi administracyjnej.

### <a name="default-resource-class"></a>Domyślna klasa zasobów
Domyślnie każdy użytkownik jest członkiem klasy zasobu małych **smallrc**. 

### <a name="resource-class-precedence"></a>Pierwszeństwo klasy zasobu
Użytkownicy mogą być członkami wielu klas zasobów. Jeśli użytkownik należy do więcej niż jedną klasę zasobów:

- Klasy zasobu dynamicznego mają pierwszeństwo przed klas statycznych zasobów. Na przykład jeśli użytkownik jest członkiem mediumrc(dynamic) i staticrc80 (statyczny), zapytania uruchamiane z mediumrc.
- Większe klasy zasobu mają pierwszeństwo przed mniejszych klasy zasobów. Na przykład jeśli użytkownik jest członkiem mediumrc i largerc, zapytania uruchamiane z largerc. Podobnie jeśli użytkownik jest członkiem staticrc20 i statirc80, zapytania uruchamiane z staticrc80 alokacji zasobów.

### <a name="queries-exempt-from-resource-classes"></a>Zapytania wykluczone z klasy zasobu
Niektóre kwerendy są zawsze uruchamiane w klasie zasobu smallrc nawet, jeśli użytkownik jest członkiem większych klasy zasobów. Te wykluczone zapytania nie wchodzą w skład limit współbieżności. Na przykład jeśli limit współbieżności 16, wielu użytkowników może wybierając z widoków systemowych bez wpływu na gniazd dostępnych współbieżności.

Poniższe instrukcje są wykluczone z klasy zasobów i są zawsze uruchamiane w smallrc:

* Utwórz lub DROP TABLE
* INSTRUKCJA ALTER TABLE... PRZEŁĄCZNIK, podziału lub SCALENIA PARTYCJI
* ALTER INDEX WYŁĄCZ
* INDEKS
* Utwórz, aktualizacji lub DROP STATISTICS
* OBCIĄĆ TABELI
* INSTRUKCJA ALTER AUTORYZACJI
* UTWÓRZ DANE LOGOWANIA
* CREATE, ALTER i DROP USER
* CREATE, ALTER i DROP procedury
* Utwórz lub PORZUĆ widok
* WSTAW WARTOŚCI
* Wybierz z widoków systemowych i widoków DMV
* WYJAŚNIĆ
* POLECENIE DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

## <a name="recommendations"></a>Zalecenia
Firma Microsoft zaleca się tworzenie użytkownika służącego do uruchamiania określonego typu zapytania lub załadować operacji. Następnie nadaj użytkownika klasę zasobu o stały zamiast klasy zasobów częste zmiany. Biorąc pod uwagę, że klas statycznych zasobów zapewniają większą kontrolę ogólną obciążenia pracą również sugerować się przy użyciu tych pierwszy przed uwzględnieniu klasy zasobu dynamicznego.

### <a name="resource-classes-for-load-users"></a>Klasy zasobów dla obciążenia użytkownikami
`CREATE TABLE`używa klastrowane indeksy magazynu kolumn domyślnie. Kompresowanie danych do magazynu kolumn indeksu jest operacją intensywnie pamięci i wykorzystania pamięci może zmniejszyć jakości indeksu. W związku z tym najprawdopodobniej podczas ładowania danych będą musieli wyższej klasy zasobów. Aby zapewnić, że obciążenie ma za mało pamięci, można utworzyć użytkownika, który został wybrany do uruchamiania obciążeń i przypisz tego użytkownika do wyższych klasy zasobów.

Pamięci niezbędnego do przetworzenia wydajne obciążenia zależy od charakteru tabeli załadowane i rozmiar danych. Aby uzyskać więcej informacji o ilości pamięci, zobacz [maksymalizacja jakości i](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md).

Po określeniu wymagania dotyczące pamięci, określ, czy można przypisać użytkownika obciążenia do klasy statyczne lub dynamiczne zasobów.

- Używanie klasy statyczne zasobów, gdy wymagania dotyczące pamięci tabeli mieszczą się w określonym zakresie. Uruchamianie obciążeń z odpowiedniej ilości pamięci. Skalowanie w magazynie danych, obciążenia nie ma potrzeby większej ilości pamięci. Za pomocą klasy statyczne zasobów, alokacji pamięci pozostają stałe. To spójność oszczędza pamięci i umożliwia równoczesne uruchamianie więcej kwerendy. Zaleca się stosowanie nowych rozwiązań używał klas statycznych zasobów najpierw te zapewniają większą kontrolę.
- Używanie klasy zasobu dynamicznego, gdy wymagania dotyczące pamięci tabeli różnią. Obciążenie może wymagać więcej pamięci niż bieżącej wartości DWU lub poziom cDWU udostępnia. W związku z tym skalowanie w magazynie danych dodaje większej ilości pamięci do operacji obciążenia, dzięki czemu obciążenia mogą szybciej.

### <a name="resource-classes-for-queries"></a>Klasy zasobów dla zapytań

Niektóre zapytania są obliczeniowych, a niektóre nie są.  

- Wybierz klasę zasobu dynamicznego zapytania skomplikowane, ale nie ma potrzeby współbieżności wysoki.  Na przykład generowania raportów codziennie lub co tydzień jest okazjonalne potrzebę zasobów. Jeśli raporty są przetwarzania dużych ilości danych, skalowanie w magazynie danych zawiera więcej pamięci do istniejącej klasy zasobów użytkownika.
- Wybierz klasę zasobu o statycznych, kiedy oczekiwań zasobów różnią się w ciągu dnia. Na przykład klasa zasobu statycznych dobrze działa w przypadku magazynu danych jest poddawany kwerendzie przez wiele osób. Skalowanie w magazynie danych, nie powoduje zmiany ilość pamięci przydzielonej dla użytkownika. W rezultacie więcej zapytania mogą być wykonywane równolegle w systemie.

Wybranie grant prawidłowego pamięci zależy od wielu czynników, takich jak ilość danych pobieranych schematy tabeli i różnych sprzężenia, wybierz, a grupa predykatów. Ogólnie rzecz biorąc przydzielenie większej ilości pamięci umożliwia kwerendy szybciej, ale zmniejsza ogólną współbieżności. Współbieżność nie stanowi to problemu, nadmierne przydzielanie pamięci nie uszkodzić przepływności. 

Do dopasowywania wydajności, należy użyć klasy innego zasobu. Następny zapewnia sekcji procedury przechowywanej, która pomaga ustalić najlepsze klasy zasobów.

## <a name="example-code-for-finding-the-best-resource-class"></a>Przykładowy kod służący do znajdowania najlepsze klasy zasobów
 
Poniższe procedury składowanej służy do ustalenia grant współbieżności i pamięć dla każdej klasy zasobu w danym celu SLO i najlepsze najbliższej klasy zasobu operacje o znacznym wykorzystaniu WIK pamięci niepartycjonowany WIK tabeli w klasie zasobu:

W tym miejscu jest celem tej procedury składowanej:  
1. Aby wyświetlić współbieżności i pamięci przyznać na klasy zasobu w danym celu SLO. Użytkownik musi podać wartości NULL tablename i schematu, jak pokazano w poniższym przykładzie.  
2. Aby wyświetlić najbliższej klasy zasobów najlepsze WIK pamięć operacji (obciążenia, tabelę kopiowania odbudować indeksu, itp.) na WIK z systemem innym niż partycjonowanej tabeli w klasie zasobu. Przechowywanej używa schematu tabeli, aby dowiedzieć się, przydział wymagany pamięci.

### <a name="dependencies--restrictions"></a>Zależności i ograniczeń:
- Aby obliczyć wymagania dotyczące pamięci dla tabeli partycjonowanej WIK nie obsługuje tej procedury składowanej.    
- Ta procedura składowana nie przyjmuje wymagania dotyczące pamięci pod uwagę dla części SELECT CTAS/INSERT-wybierz przyjęto założenie, że jest SELECT.
- Tę procedurę składowaną używa tabeli tymczasowej, która jest dostępna w sesji, gdy ta procedura składowana została utworzona.    
- Tę procedurę składowaną zależy od bieżącego ofert (na przykład konfiguracja sprzętu, konfiguracji DMS), a w przypadku zmiany dowolnego tego następnie tego przechowywanej nie działa prawidłowo.  
- Tę procedurę składowaną zależy od istniejących limit oferowany współbieżności i jeśli zmieni się który następnie tej procedury składowanej nie będzie działało poprawnie.  
- Tę procedurę składowaną zależy od istniejących ofert klasy zasobów i jeśli zmieni się który następnie tej procedury składowanej nie będzie działało poprawnie.  

>  [!NOTE]  
>  Jeśli po wykonaniu procedury składowanej z parametrami podany nie otrzymują danych wyjściowych, następnie mogą występować dwa. <br />1. Parametr albo DW zawiera nieprawidłową wartość SLO <br />2. Lub, nie nie zgodnej klasy zasobu dla operacji WIK w tabeli. <br />Na przykład w DW100, najwyższy dostępny przydział pamięci to 400 MB, a schemat tabeli ma całego wystarczającą przetnie wymaganie 400 MB.
      
### <a name="usage-example"></a>Przykład użycia:
Składnia:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Należy podać parametr o wartości NULL do wyodrębnienia bieżącej wartości DWU z bazy danych magazynu danych lub podaj wszystkie obsługiwane DWU w postaci "DW100"
2. @SCHEMA_NAME:Podaj nazwę schematu tabeli
3. @TABLE_NAME:Podaj nazwę tabeli odsetek

Przykłady wykonywania tej procedury przechowywanej:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Poniższa instrukcja tworzy Tabela1, który jest używany w powyższych przykładach.
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

### <a name="stored-procedure-definition"></a>Definicja procedury składowanej

```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(@DWU VARCHAR(7),
 @SCHEMA_NAME VARCHAR(128),
 @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temp table (CTAS) to hold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```




## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zarządzaniu bazy danych użytkowników i zabezpieczeń, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Aby uzyskać więcej informacji na temat sposobu większe grupy zasobów może zwiększyć jakość indeksu klastrowanego magazynu kolumn, zobacz [optymalizacji pamięci magazynu kolumn kompresji](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md).

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Rebuilding indexes to improve segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
