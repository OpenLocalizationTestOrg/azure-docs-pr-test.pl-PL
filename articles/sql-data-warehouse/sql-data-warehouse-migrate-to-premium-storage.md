---
title: "aaaMigrate magazynu toopremium magazynu istniejących danych Azure | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące migracji istniejącego magazynu toopremium magazynu danych"
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
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Migracja magazynu toopremium magazynu danych
Usługa Azure SQL Data Warehouse niedawno wprowadzone [magazyn w warstwie premium dla większej wydajności przewidywalności][premium storage for greater performance predictability]. Istniejące dane, które można teraz magazynów obecnie magazynu w warstwie standardowa migracji toopremium magazynu. Możesz korzystać z automatycznych migracji, lub jeśli wolisz toocontrol podczas toomigrate (które obejmują przestój), możesz zrobić samodzielnie hello migracji.

Jeśli masz więcej niż jeden magazyn danych, użyj hello [harmonogramu automatycznej migracji] [ automatic migration schedule] toodetermine podczas również zostaną poddane migracji.

## <a name="determine-storage-type"></a>Określanie typu magazynu
Jeśli utworzono hurtowni danych przed powitania po daty są aktualnie używa magazynu w warstwie standardowa.

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
Domyślnie, przeprowadzimy migrację bazy danych dla Ciebie między 6:00 a 6:00:00 czasu lokalnego w Twoim regionie podczas hello [harmonogramu automatycznej migracji][automatic migration schedule]. Podczas migracji hello będzie można jej używać istniejącego magazynu danych. Witaj migracji zajmie około jednej godziny na terabajt magazynu na magazyn danych. Nie zostanie obciążona podczas jakiejkolwiek jego części hello automatyczną migrację.

> [!NOTE]
> Po zakończeniu migracji hello magazynu danych będzie ponownie online i można go użyć.
>
>

Microsoft trwa powitania po migracji hello toocomplete czynności (te nie wymagają żadnych zaangażowania ze strony użytkownika). W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."

1. Microsoft zmienia "MyDW" za "MyDW_DO_NOT_USE_ [sygnatury czasowej]".
2. Microsoft wstrzymuje "MyDW_DO_NOT_USE_ [sygnatury czasowej]". W tym czasie wykonywana jest kopia zapasowa. Wiele pauzy i wznawia mogą pojawić się firma Microsoft napotkania problemów podczas tego procesu.
3. Microsoft tworzy nowy magazyn danych o nazwie "MyDW" na magazyn w warstwie premium z kopii zapasowej hello w kroku 2. "MyDW" pojawią się dopiero po zakończeniu przywracania hello.
4. Po zakończeniu przywracania hello "MyDW" zwraca toohello tych samych danych jednostek magazynu i stan (wstrzymana lub aktywnym), który był przed migracją hello.
5. Po zakończeniu migracji hello Microsoft usuwa "MyDW_DO_NOT_USE_ [sygnatury czasowej]".

> [!NOTE]
> Witaj poniższe ustawienia nie jest przenoszone w ramach migracji hello:
>
> * Inspekcji na poziomie bazy danych hello musi toobe ponownie włączona.
> * Reguły zapory na poziomie bazy danych hello muszą toobe ponownie dodane. Reguły zapory na poziomie serwera hello nie dotyczy.
>
>

### <a name="automatic-migration-schedule"></a>Automatyczna migracja harmonogramu
Migracje automatyczne występują między 6:00 a 6:00:00 (czas lokalny dla regionu) podczas hello według harmonogramu awarii.

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

## <a name="self-migration-toopremium-storage"></a>Samodzielna migracji toopremium magazynu
Jeśli chcesz toocontrol, gdy nastąpi z przestoju, można użyć hello następujące kroki toomigrate istniejącego magazynu danych w magazynie toopremium magazynu w warstwie standardowa. Jeśli wybierzesz tę opcję, należy wykonać migracji własny hello przed rozpoczęciem powitalne automatycznej migracji w tym regionie. Dzięki temu, że uniknąć ryzyka hello automatycznej migracji powoduje konflikt (zobacz toohello [harmonogramu automatycznej migracji][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instrukcje dotyczące migracji samodzielnej
toomigrate danych magazynu samodzielnie, użyj hello kopii zapasowej i przywracania funkcji. Hello przywracania część migracji hello jest oczekiwany tootake około jednej godziny na terabajt magazynu na magazyn danych. Witaj tookeep takie same nazwy, po zakończeniu migracji, należy wykonać hello [toorename kroki podczas migracji][steps toorename during migration].

1. [Wstrzymaj] [ Pause] magazynu danych. Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.
2. [Przywróć] [ Restore] z najnowszych migawki.
3. Usuwanie istniejącego magazynu danych na magazynu w warstwie standardowa. **Jeśli nie toodo ten krok zostanie naliczona opłata dla obu magazynów danych.**

> [!NOTE]
> Witaj poniższe ustawienia nie jest przenoszone w ramach migracji hello:
>
> * Inspekcji na poziomie bazy danych hello musi toobe ponownie włączona.
> * Reguły zapory na poziomie bazy danych hello muszą toobe ponownie dodane. Reguły zapory na poziomie serwera hello nie dotyczy.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Zmień nazwę magazynu danych podczas migracji (opcjonalnie)
Dwie bazy danych na powitania nie może być tym samym serwerze logicznym hello tej samej nazwy. Magazyn danych SQL obsługuje teraz hello toorename możliwości magazynu danych.

W tym przykładzie załóżmy, że istniejącego magazynu danych na magazynu w warstwie standardowa aktualnie ma nazwę "MyDW."

1. Zmień nazwę "MyDW" za pomocą następującego polecenia ALTER DATABASE hello. (W tym przykładzie firma Microsoft będzie zmień jego nazwę "MyDW_BeforeMigration.")  To polecenie zatrzymania wszystkich istniejących transakcji i musi zostać wykonane w hello toosucceed bazy danych master.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Wstrzymaj] [ Pause] "MyDW_BeforeMigration." Kliknięcie tej pozycji spowoduje automatyczne kopie zapasowe.
3. [Przywróć] [ Restore] z najnowszych migawki nową bazę danych o nazwie hello on toobe (na przykład "MyDW").
4. Usuń "MyDW_BeforeMigration." **Jeśli nie toodo ten krok zostanie naliczona opłata dla obu magazynów danych.**


## <a name="next-steps"></a>Następne kroki
Bez hello zmienić toopremium magazynu, należy również zwiększonej liczby plików bazy danych obiektów blob w hello podstawowej architektury magazynu danych. zwiększenia wydajności hello toomaximize tę zmianę, Odbuduj Twojej klastrowane indeksy magazynu kolumn za pomocą następującego skryptu hello. skrypt Hello działa, powodując, że niektóre istniejące dane toohello dodatkowe obiektów blob. Jeśli nie podejmiesz żadnych działań, danych hello naturalnie zostanie ponownie rozesłać wraz z upływem czasu, ponieważ załadowanie większej ilości danych w tabelach.

**Wymagania wstępne:**

- Witaj magazynu danych należy uruchamiać z jednostki magazynu danych 1000 lub nowszą (zobacz [mocy obliczeniowej skali][scale compute power]).
- Witaj wykonywania skryptu hello użytkownika powinna mieć hello [roli mediumrc] [ mediumrc role] lub nowszej. tooadd toothis roli użytkownika, wykonaj następujące hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
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

Jeśli wystąpią problemy z magazynem danych, [Utwórz bilet pomocy technicznej] [ create a support ticket] i referencyjne "Magazyn toopremium migracji" jako hello z możliwych przyczyn.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
