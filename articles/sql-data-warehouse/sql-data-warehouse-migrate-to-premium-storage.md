---
title: "Migrację istniejącego magazynu danych Azure do magazynu premium | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące migracji istniejącego magazynu danych do magazynu w warstwie premium"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a>Migracja magazynu danych do magazynu w warstwie premium
Usługa Azure SQL Data Warehouse niedawno wprowadzone [magazyn w warstwie premium dla większej wydajności przewidywalności][premium storage for greater performance predictability]. Teraz można migrować istniejące magazynów danych obecnie na magazynu w warstwie standardowa do magazyn w warstwie premium. Możesz korzystać z automatycznych migracji, lub jeśli wolisz decyduje o migracji (która jest związana z przestój), migrację można wykonać samodzielnie.

Jeśli masz więcej niż jeden magazyn danych, użyj [harmonogramu automatycznej migracji] [ automatic migration schedule] ustalenie, kiedy zostanie ono również zmigrowane.

## <a name="determine-storage-type"></a>Określanie typu magazynu
Jeśli magazyn danych został utworzony przed następujących dat, są aktualnie używa magazynu w warstwie standardowa.

| **Region** | **Utworzone przed tą datą magazynu danych** |
|:--- |:--- |
| Australia Wschodnia |Magazyn w warstwie Premium nie są jeszcze dostępne |
| Chiny Wschodnie |1 listopada 2016 r. |
| Chiny Północne |1 listopada 2016 r. |
| Niemcy Środkowe |1 listopada 2016 r. |
| Niemcy Północno-Wschodnie |1 listopada 2016 r. |
| Indie Zachodnie |Magazyn w warstwie Premium nie są jeszcze dostępne |
| Japonia Zachodnia |Magazyn w warstwie Premium nie są jeszcze dostępne |
| Środkowo-północne stany USA |10 listopada 2016 r. |

## <a name="automatic-migration-details"></a>Szczegóły automatycznej migracji
Domyślnie, przeprowadzimy migrację bazy danych dla Ciebie między 6:00 a 6:00:00 w Twoim regionie czasu lokalnego, podczas [harmonogramu automatycznej migracji][automatic migration schedule]. Podczas migracji będzie można jej używać istniejącego magazynu danych. Migracji zajmie około jednej godziny na terabajt magazynu na magazyn danych. Nie zostanie obciążona podczas jakiejkolwiek jego części automatyczną migrację.

> [!NOTE]
> Po zakończeniu migracji magazynu danych będzie ponownie online i można go użyć.
>
>

Microsoft podejmuje następujące kroki, aby ukończyć migrację (te nie wymagają żadnych zaangażowania ze strony użytkownika). W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."

1. Microsoft zmienia nazwę "MyDW" do "MyDW_DO_NOT_USE_ [sygnatury czasowej]".
2. Microsoft wstrzymuje "MyDW_DO_NOT_USE_ [sygnatury czasowej]". W tym czasie wykonywana jest kopia zapasowa. Wiele pauzy i wznawia mogą pojawić się firma Microsoft napotkania problemów podczas tego procesu.
3. Microsoft tworzy nowy magazyn danych o nazwie "MyDW" na magazyn w warstwie premium z kopii zapasowej wykonanej w kroku 2. "MyDW" pojawią się dopiero po zakończeniu przywracania.
4. Po zakończeniu przywracania, "MyDW" zwraca do tej samej jednostki magazynu danych i stanu (wstrzymana lub aktywnym) aby był przed migracją.
5. Po zakończeniu migracji Microsoft usuwa "MyDW_DO_NOT_USE_ [sygnatury czasowej]".

> [!NOTE]
> Poniższe ustawienia nie przenoszone w ramach migracji:
>
> * Inspekcji na poziomie bazy danych należy ponownie włączyć.
> * Reguły zapory na poziomie bazy danych należy ponownie dodać. Nie wpływają na reguły zapory na poziomie serwera.
>
>

### <a name="automatic-migration-schedule"></a>Automatyczna migracja harmonogramu
Migracje automatyczne występują między 6:00 a 6:00:00 (czas lokalny dla regionu) podczas do następującego harmonogramu awarii.

| **Region** | **Szacowana data rozpoczęcia** | **Szacowana data końcowa** |
|:--- |:--- |:--- |
| Australia Wschodnia |Nie można ustalić jeszcze |Nie można ustalić jeszcze |
| Chiny Wschodnie |9 stycznia 2017 r. |13 stycznia 2017 r. |
| Chiny Północne |9 stycznia 2017 r. |13 stycznia 2017 r. |
| Niemcy Środkowe |9 stycznia 2017 r. |13 stycznia 2017 r. |
| Niemcy Północno-Wschodnie |9 stycznia 2017 r. |13 stycznia 2017 r. |
| Indie Zachodnie |Nie można ustalić jeszcze |Nie można ustalić jeszcze |
| Japonia Zachodnia |Nie można ustalić jeszcze |Nie można ustalić jeszcze |
| Środkowo-północne stany USA |9 stycznia 2017 r. |13 stycznia 2017 r. |

## <a name="self-migration-to-premium-storage"></a>Samodzielna migracji magazyn w warstwie premium
Jeśli chcesz kontrolować gdy nastąpi z przestoju, można użyć następujące kroki migracji istniejącego magazynu danych na standardowy magazyn na magazyn w warstwie premium. Wybierz tę opcję, należy wypełnić własny migracji, przed rozpoczęciem automatycznej migracji, w tym regionie. Dzięki temu, że uniknąć ryzyka automatycznej migracji powoduje konflikt (dotyczą [harmonogramu automatycznej migracji][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instrukcje dotyczące migracji samodzielnej
Aby samodzielnie migracji magazynu danych, użyj kopii zapasowej i przywracania funkcji. Przywracanie część migracji powinien zająć około jednej godziny na terabajt magazynu na magazyn danych. Jeśli chcesz zachować tę samą nazwę, po zakończeniu migracji, należy wykonać [instrukcje dotyczące zmiany nazwy podczas migracji][steps to rename during migration].

1. [Wstrzymaj] [ Pause] magazynu danych. Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.
2. [Przywróć] [ Restore] z najnowszych migawki.
3. Usuwanie istniejącego magazynu danych na magazynu w warstwie standardowa. **Jeśli nie wykonać ten krok, zostanie naliczona opłata dla obu magazynów danych.**

> [!NOTE]
> Poniższe ustawienia nie przenoszone w ramach migracji:
>
> * Inspekcji na poziomie bazy danych należy ponownie włączyć.
> * Reguły zapory na poziomie bazy danych należy ponownie dodać. Nie wpływają na reguły zapory na poziomie serwera.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Zmień nazwę magazynu danych podczas migracji (opcjonalnie)
Dwie bazy danych na tym samym serwerze logicznym nie może mieć takiej samej nazwie. Magazyn danych SQL obsługuje teraz możliwość zmiany nazwy magazynu danych.

W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."

1. Zmień nazwę "MyDW" za pomocą następującego polecenia ALTER DATABASE. (W tym przykładzie firma Microsoft będzie zmień jego nazwę "MyDW_BeforeMigration.")  To polecenie zatrzymuje wszystkich istniejących transakcji i musi zostać wykonane w bazie danych master została wykonana pomyślnie.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Wstrzymaj] [ Pause] "MyDW_BeforeMigration." Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.
3. [Przywróć] [ Restore] z najbardziej aktualną migawki nową bazę danych o nazwie on używany jako (na przykład "MyDW").
4. Usuń "MyDW_BeforeMigration." **Jeśli nie wykonać ten krok, zostanie naliczona opłata dla obu magazynów danych.**


## <a name="next-steps"></a>Następne kroki
W przypadku zmiany do magazynu w warstwie premium masz również zwiększonej liczby plików bazy danych obiektów blob w podstawowej architektury magazynu danych. Aby zmaksymalizować korzyści w zakresie wydajności tej zmiany, należy ponownie utworzyć Twoje klastrowane indeksy magazynu kolumn przy użyciu następującego skryptu. Działania skryptu, wymuszając istniejące dane na dodatkowe obiekty BLOB. Jeśli nie podejmiesz żadnych działań, dane naturalnie zostanie ponownie rozesłać wraz z upływem czasu, ponieważ załadowanie większej ilości danych w tabelach.

**Wymagania wstępne:**

- Magazyn danych powinno być ono uruchomione i jednostki magazynu danych 1000 lub nowszą (zobacz [mocy obliczeniowej skali][scale compute power]).
- Musi należeć do użytkownika wykonywania skryptu [roli mediumrc] [ mediumrc role] lub nowszej. Aby dodać użytkownika do tej roli, wykonaj następujące czynności:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Jeśli wystąpią problemy z magazynem danych, [Utwórz bilet pomocy technicznej] [ create a support ticket] odwołanie "migracji do magazyn w warstwie premium" jako możliwe przyczyny i.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
