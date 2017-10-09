---
title: "aaaSQL bazy danych — automatycznego dostrajania | Dokumentacja firmy Microsoft"
description: "Baza danych SQL analizuje zapytania SQL i automatycznie dostosowuje toouser obciążenia."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Automatyczne dostrajanie

Baza danych SQL Azure to usługa danych pełni zarządzana, która monitoruje hello zapytań, które są wykonywane na powitania bazy danych i automatycznie może zwiększyć wydajność obciążeń hello. Baza danych SQL Azure ma mechanizm wbudowane narzędzie analizy, który można automatycznie dostrojenie i poprawić wydajność kwerend przez dynamicznie dostosowanie hello bazy danych tooyour obciążenia. Automatycznego dostrajania w bazie danych SQL Azure może być jednym z hello najważniejszych funkcji, które można włączyć na bazie danych SQL Azure toooptimize wydajność kwerend.

Znajduje się w artykule kroki hello zbyt[Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md) przy użyciu hello portalu Azure.

## <a name="why-automatic-tuning"></a>Dlaczego automatycznego dostrajania?

Jedną z głównych zadań hello w administracji klasycznego bazy danych jest monitorowanie obciążenia hello identyfikowanie krytyczne SQL zapytań indeksów, które powinny zostać dodane tooimprove wydajności, a rzadko używane indeksów. Baza danych SQL Azure zapewnia wgląd szczegółowe w hello kwerend i indeksów należy toomonitor. Jednak nieprzerwane monitorowanie bazy danych jest trudnym i żmudnym zadaniem, szczególnie w przypadku pracy z wieloma bazami danych. Zarządzanie olbrzymią liczbę baz danych może być niemożliwe toodo wydajnie nawet w przypadku wszystkie dostępne narzędzia i raporty zawierające bazy danych SQL Azure i portalu Azure. Zamiast monitorowania i dostrajania bazę danych ręcznie, warto rozważyć delegowanie niektóre hello monitorowania i dostrajania tooAzure działania bazy danych SQL przy użyciu funkcji automatycznego dostrajania. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Jak działa automatycznego dostrajania?

Baza danych SQL Azure ma wydajności ciągłego monitorowania i analizy procesu, który stale uzyskuje informacje o hello charakterystyczne dla obciążenia i identyfikować potencjalne problemy i ulepszenia.

![Proces automatycznego dostrajania](./media/sql-database-automatic-tuning/tuning-process.png)

Ta umożliwia procesu toodynamically bazy danych SQL Azure dostosowania tooyour obciążenia przez wyszukiwanie jaki indeksy i planów może zwiększyć wydajność obciążeń i indeksuje co wpływa na obciążeń. W oparciu o te wyniki, automatycznego dostrajania stosuje dostrajania akcje, które poprawiają wydajność obciążenia. Ponadto bazy danych SQL Azure stale monitoruje wydajności po każdej zmianie przez automatycznego dostrajania tooensure zwiększa wydajność obciążenia. Dowolną akcję, która nie poprawić wydajność zostanie automatycznie przywrócony. Ten proces sprawdzania poprawności jest kluczowym elementem, który zapewnia, że wszelkie zmiany wprowadzone przez automatycznego dostrajania nie można jej zmniejszyć wydajność hello obciążenia.

Istnieją dwa automatycznego dostrajania aspektów, które są dostępne w bazie danych SQL Azure:

 -  **Zarządzanie indeksami automatyczne** , które identyfikują indeksów, które mają zostać dodane w bazie danych i indeksów, które powinny zostać usunięte.
 -  **Automatyczne plan korekty** (wkrótce, już dostępne w 2017 serwera SQL), które identyfikują planów powodować problemy i poprawek SQL zaplanować problemy z wydajnością.

## <a name="automatic-index-management"></a>Zarządzanie indeksami automatyczne

W bazie danych SQL Azure Zarządzanie indeksami jest łatwe, ponieważ baza danych SQL Azure uzyskuje informacje o obciążenia i zapewnia, że danych jest zawsze optymalnie indeksowane. Indeks właściwy projekt ma kluczowe znaczenie dla uzyskania optymalnej wydajności obciążenie i indeksu automatycznego zarządzania mogą pomóc w Optymalizuj indeksy użytkownika. Indeks automatycznego zarządzania można rozwiązać problemy z wydajnością w niepoprawnie indeksowanego baz danych, lub Obsługa i poprawić indeksy na powitania istniejący schemat bazy danych. 

### <a name="why-do-you-need-index-management"></a>Dlaczego należy Zarządzanie indeksami?

Indeksy przyspieszenia niektórych kwerend odczytujących dane z tabel hello; jednak mogą one spowolnić hello zapytań, które aktualizują dane. Należy toocarefully analizowanie, gdy toocreate indeksu i jakie kolumny należy tooinclude w hello indeksu. Niektóre indeksy nie mogą być wymagane po pewnym czasie. W związku z tym musisz tooperiodically zidentyfikować i Porzuć indeksy hello, które nie powodują żadnych korzyści. Jeśli zignorujesz hello nieużywane indeksów, czy zmniejszyć wydajność kwerend hello, które aktualizują dane bez żadnych korzyści na powitania zapytań, które odczytanie danych. Nieużywane indeksów również na ogólną wydajność systemu hello, ponieważ dodatkowe aktualizacje wymagają niepotrzebnych rejestrowania.

Znajdowanie hello optymalny zestaw indeksów, które zwiększają wydajność kwerend hello, odczytywanie danych z tabel, które ma minimalny wpływ na aktualizacje mogą wymagać ciągły i złożone analizy.

Baza danych SQL Azure używa wbudowane narzędzie analizy i zaawansowanych reguł, które analizuje zapytania, zidentyfikuj indeksów, które są optymalne dla bieżącej obciążeń i indeksów hello może zostać usunięta. Baza danych SQL Azure gwarantuje, że niezbędne minimalny zbiór indeksów, które zoptymalizować hello zapytania, które zapoznały danych, z hello zminimalizować wpływ na hello inne zapytania.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Jak tooidentify indeksy tego toobe należy zmienić w bazie danych?

Baza danych SQL Azure ułatwia proces zarządzania indeksu. Zamiast żmudne hello analizy ręczne obciążenia i monitorowanie indeksu bazy danych SQL Azure analizuje obciążenie, identyfikuje hello zapytań, które można wykonać szybciej z nowego indeksu i identyfikuje nieużywane lub zduplikowane indeksów. Więcej informacji o identyfikacji indeksów, które powinny zostać zmienione w [znaleźć zalecenia dotyczące indeksu w portalu Azure](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Zagadnienia dotyczące zarządzania automatyczne indeksu

Jeśli okaże się, że hello wbudowane reguły poprawić wydajność hello bazy danych, może pozwolić automatycznie Zarządzaj indeksami Twojej bazy danych Azure SQL.

Akcje wymagane toocreate indeksy niezbędne w bazach danych SQL Azure może korzystać z zasobów i tymczasowo wpłynąć na wydajność obciążenia. toominimize hello wpływ tworzenia indeksu na obciążenie wydajności bazy danych SQL Azure umożliwia znalezienie hello przedział czasu odpowiednie do żadnej operacji zarządzania indeksu. Dostrajanie akcji jest odroczone, jeśli baza danych hello musi tooexecute zasobów obciążenia i uruchomiony, gdy hello bazy danych ma wystarczającą ilość nieużywanych zasobów, które mogą być używane dla zadania konserwacji hello. Jedna ważnych funkcji w indeksie automatycznego zarządzania jest weryfikacja hello akcje. Gdy baza danych SQL Azure tworzy lub porzuca indeks, proces monitorowania analizuje wydajności z tooverify obciążenia, czy akcja hello wyższą wydajność hello. Jeśli nie przyniesie znaczne ulepszenia — Akcja hello natychmiast zostanie przywrócony. Dzięki temu bazy danych SQL Azure zapewnia, że akcje automatyczne niekorzystnie wpłynąć na wydajność obciążenia. Utworzone przez automatyczne dostrajanie indeksów są niewidoczne dla operacji obsługi hello na powitania podstawowej schematu. Zmiany schematu, takie jak porzucenie lub zmienianie nazw kolumn nie są blokowane przez hello obecności Indeksy tworzone automatycznie. Indeksów, które są automatycznie tworzone przez usługę Azure SQL Database są usuwane natychmiast, kiedy związane z tabeli lub kolumny jest porzucany.

## <a name="automatic-plan-choice-correction"></a>Planowanie automatycznego wyboru korekty

Automatyczne plan korekty jest nową funkcją automatycznego dostrajania dodany do programu SQL Server 2017 CTP2.0 identyfikujący planów SQL, które błędne działanie. Opcja automatycznego dostrajania będzie wkrótce dostępne w bazie danych SQL Azure. Aby uzyskać więcej informacji o [automatycznego dostrajania w programu SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Następne kroki

- tooenable automatycznego dostrajania w bazie danych SQL Azure i umożliwiają automatyczne dostrajania funkcji w pełni zarządzać obciążenie, zobacz [Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md).
- toouse ręczne dostrajanie możesz przejrzeć [dostrajanie zalecenia w portalu Azure](sql-database-advisor-portal.md) i ręcznie zastosować hello te, które poprawić wydajność kwerend.
