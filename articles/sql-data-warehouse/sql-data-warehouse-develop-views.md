---
title: "Widoki aaaUsing T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z widoków języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Widoki w usłudze SQL Data Warehouse
Widoki są szczególnie przydatne w usłudze SQL Data Warehouse. Służy na kilka różnych sposobów tooimprove hello jakości rozwiązania.  W tym artykule omówiono kilka przykładów sposobu tooenrich rozwiązania z widoków, a także ograniczenia hello, które wymagają toobe traktowane jako.

> [!NOTE]
> Składnia `CREATE VIEW` nie została szczegółowo opisana w tym artykule. Zobacz toohello [CREATE VIEW] [ CREATE VIEW] artykuł w witrynie MSDN, aby uzyskać informacje na ten.
> 
> 

## <a name="architectural-abstraction"></a>Abstrakcja architektury
Bardzo typowy wzorzec aplikacji jest toore — Tworzenie tabel za pomocą tworzenia tabeli jako wybierz (CTAS) następuje zmiana nazwy wzorzec podczas ładowania danych obiektu.

w poniższym przykładzie Hello dodaje wymiaru daty tooa rekordów nową datą. Należy zwrócić uwagę, jak nowy tabela, DimDate_New, utworzenia i zmienić nazwy oryginalnej wersji hello tooreplace hello tabeli.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Jednak ta metoda może spowodować tabel znajdujących się i znika z punktu widzenia użytkownika, a także "Tabela nie istnieje" komunikaty o błędach. Widoki może być używane tooprovide użytkowników z warstwą prezentacji spójne przy jednoczesnym obiektów hello zostały zmienione. Zapewniając użytkownikom dostęp do danych toohello za pośrednictwem widoków, oznacza, że użytkownicy nie muszą toohave widoczność hello tabel. Zapewnia to spójny interfejs użytkownika przy jednoczesnym zapewnieniu projektanci magazynu danych hello może rozwijać hello modelu danych i zmaksymalizować wydajność przy użyciu CTAS podczas procesu ładowania danych hello.    

## <a name="performance-optimization"></a>Optymalizacja wydajności
Widoki mogą być również wykorzystywane tooenforce zoptymalizowanych pod kątem wydajności sprzężenia między tabelami. Na przykład widoku można zastosować klucza dystrybucji nadmiarowe jako część hello dołączenie przenoszenia danych toominimize kryteriów.  Inną zaletą widok może być tooforce określonej kwerendy lub łącząca wskazówki. Korzystanie z widoków w ten sposób gwarantuje, że sprzężenia zawsze są realizowane w sposób optymalny unikanie hello potrzebę prawidłowa konstrukcja hello tooremember użytkowników dla ich sprzężeń.

## <a name="limitations"></a>Ograniczenia
Widoki w usłudze SQL Data Warehouse są tylko metadane.  W związku z tym hello następujące opcje nie są dostępne:

* Nie jest dostępna opcja powiązanie schematu
* Nie można aktualizować tabel podstawowych za pośrednictwem widoku hello
* Nie można tworzyć widoki w tabelach tymczasowych
* Nie jest obsługiwane dla hello ROZWIJANIA / wskazówki NOEXPAND
* Brak widoków indeksowanych w usłudze SQL Data Warehouse

## <a name="next-steps"></a>Następne kroki
Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].
Aby uzyskać `CREATE VIEW` składni można znaleźć zbyt[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
