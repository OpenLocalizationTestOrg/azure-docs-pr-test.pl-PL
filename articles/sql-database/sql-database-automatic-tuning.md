---
title: "Baza danych SQL — automatycznego dostrajania | Dokumentacja firmy Microsoft"
description: "Baza danych SQL analizuje zapytania SQL i automatycznie dostosowuje się do użytkownika obciążenia."
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
ms.openlocfilehash: f5552793db2d89542782b7d9e8f996314f62e429
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automatic-tuning"></a>Automatyczne dostrajanie

Baza danych SQL Azure to usługa danych pełni zarządzana, która monitoruje zapytań, które są wykonywane na bazie danych i automatycznie może poprawić wydajność obciążenia. Baza danych SQL Azure ma mechanizm wbudowane narzędzie analizy, który można automatycznie dostrojenie i poprawić wydajność kwerend przez dynamicznie dostosowanie bazy danych, aby obciążenie. Automatycznego dostrajania w bazie danych SQL Azure może być jedną z najważniejszych funkcji, możesz włączyć w bazie danych SQL Azure w celu zoptymalizowania wydajności zapytań.

Zobacz ten artykuł, aby uzyskać instrukcje dotyczące [Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md) przy użyciu portalu Azure.

## <a name="why-automatic-tuning"></a>Dlaczego automatycznego dostrajania?

Jedną z głównych zadań w witrynie Administracja klasycznego bazy danych jest monitorowanie obciążenia, identyfikowanie krytyczne zapytania SQL, indeksów, które mają zostać dodane w celu zwiększenia wydajności i indeksów rzadko używane. Baza danych SQL Azure zapewnia szczegółowy wgląd w kwerend i indeksów, które chcesz monitorować. Jednak nieprzerwane monitorowanie bazy danych jest trudnym i żmudnym zadaniem, szczególnie w przypadku pracy z wieloma bazami danych. Zarządzanie olbrzymią liczbę baz danych może być niemożliwe czy wydajnie, nawet w przypadku wszystkie dostępne narzędzia i raporty zawierające bazy danych SQL Azure i portalu Azure. Zamiast monitorowania i dostrajania bazę danych ręcznie, można rozważyć delegowanie niektóre działania monitorowania i dostrajania do bazy danych SQL Azure przy użyciu funkcji automatycznego dostrajania. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Jak działa automatycznego dostrajania?

Baza danych SQL Azure ma wydajności ciągłego monitorowania i analizy procesu, który stale uzyskuje informacje o charakterystyczne dla obciążenia i identyfikować potencjalne problemy i ulepszenia.

![Proces automatycznego dostrajania](./media/sql-database-automatic-tuning/tuning-process.png)

Ten proces umożliwia dynamiczne dostosowanie do obciążenia przez wyszukiwanie jaki indeksy i planów może zwiększyć wydajność obciążeń i indeksów, które mają wpływ na obciążeń, baza danych SQL Azure. W oparciu o te wyniki, automatycznego dostrajania stosuje dostrajania akcje, które poprawiają wydajność obciążenia. Ponadto bazy danych SQL Azure stale monitoruje wydajności po wszelkie zmiany wprowadzone przez automatycznego dostrajania, aby upewnić się, że zwiększa wydajność obciążenia. Dowolną akcję, która nie poprawić wydajność zostanie automatycznie przywrócony. Ten proces sprawdzania poprawności jest kluczowym elementem, który zapewnia, że wszelkie zmiany wprowadzone przez automatycznego dostrajania nie można jej zmniejszyć wydajność obciążenia.

Istnieją dwa automatycznego dostrajania aspektów, które są dostępne w bazie danych SQL Azure:

 -  **Zarządzanie indeksami automatyczne** , które identyfikują indeksów, które mają zostać dodane w bazie danych i indeksów, które powinny zostać usunięte.
 -  **Automatyczne plan korekty** (wkrótce, już dostępne w 2017 serwera SQL), które identyfikują planów powodować problemy i poprawek SQL zaplanować problemy z wydajnością.

## <a name="automatic-index-management"></a>Zarządzanie indeksami automatyczne

W bazie danych SQL Azure Zarządzanie indeksami jest łatwe, ponieważ baza danych SQL Azure uzyskuje informacje o obciążenia i zapewnia, że danych jest zawsze optymalnie indeksowane. Indeks właściwy projekt ma kluczowe znaczenie dla uzyskania optymalnej wydajności obciążenie i indeksu automatycznego zarządzania mogą pomóc w Optymalizuj indeksy użytkownika. Indeks automatycznego zarządzania można rozwiązać problemy z wydajnością w niepoprawnie indeksowanego baz danych, lub Obsługa i poprawić indeksy na istniejący schemat bazy danych. 

### <a name="why-do-you-need-index-management"></a>Dlaczego należy Zarządzanie indeksami?

Indeksy przyspieszenia niektórych kwerend odczytujących dane z tabel. jednak mogą one spowolnić zapytań, które aktualizują dane. Należy dokładnie analizować, kiedy należy utworzyć indeks i jakie kolumny należy uwzględnić w indeksie. Niektóre indeksy nie mogą być wymagane po pewnym czasie. W związku z tym konieczne będzie okresowo zidentyfikować i Porzuć indeksy, które nie powodują żadnych korzyści. Jeśli zignorujesz nieużywane indeksów wydajności zapytań, które aktualizują dane może zmniejszyć bez żadnych korzyści w zapytaniach, które odczytanie danych. Nieużywane indeksów również na ogólną wydajność systemu, ponieważ dodatkowe aktualizacje wymagają niepotrzebnych rejestrowania.

Znajdowanie optymalny zestaw indeksów, które zwiększają wydajność zapytań, które odczytuje dane z tabel i ma minimalny wpływ na aktualizacje mogą wymagać ciągły i złożone analizy.

Baza danych SQL Azure używa wbudowane narzędzie analizy i zaawansowanych reguł, które analizuje zapytania, zidentyfikuj indeksów, które są optymalne dla bieżącej obciążeń i indeksów może zostać usunięta. Baza danych SQL Azure zapewnia minimalny zestaw niezbędne indeksów, które zoptymalizować zapytania, które zapoznały danych w trybie zminimalizowanym wpływu na inne zapytania.

### <a name="how-to-identify-indexes-that-need-to-be-changed-in-your-database"></a>Jak zidentyfikować indeksów, które muszą zostać zmienione w bazie danych?

Baza danych SQL Azure ułatwia proces zarządzania indeksu. Zamiast żmudne analizy ręczne obciążenia i monitorowanie indeksu bazy danych SQL Azure analizuje obciążenie, identyfikuje zapytań, które można wykonać szybciej z nowego indeksu i identyfikuje nieużywane lub zduplikowane indeksów. Więcej informacji o identyfikacji indeksów, które powinny zostać zmienione w [znaleźć zalecenia dotyczące indeksu w portalu Azure](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Zagadnienia dotyczące zarządzania automatyczne indeksu

Jeśli okaże się, że wbudowane reguły poprawić wydajność bazy danych, może pozwolić automatycznie Zarządzaj indeksami Twojej bazy danych Azure SQL.

Czynności wymagane do tworzenia indeksów niezbędne w bazach danych SQL Azure może korzystać z zasobów i tymczasowo wpływać na wydajność obciążenia. Aby zminimalizować wpływ tworzenia indeksu na wydajność przetwarzania obciążenia, baza danych SQL Azure znajduje przedział czasu odpowiednie do żadnej operacji zarządzania indeksu. Dostrajanie akcji jest odroczone, jeśli baza danych musi zasoby wymagane do wykonania obciążenie i uruchomiony, gdy baza danych ma wystarczająco dużo nieużywanych zasobów, które mogą być używane dla zadań konserwacji. Jedną z ważnych funkcji w indeksie automatycznego zarządzania jest weryfikacji działań. Gdy baza danych SQL Azure tworzy lub porzuca indeks, proces monitorowania analizuje wydajność obciążenia można zweryfikować, że akcja poprawia wydajność. Jeśli nie przyniesie znaczne ulepszenia — akcja zostanie bezpośrednio przywrócony. Dzięki temu bazy danych SQL Azure zapewnia, że akcje automatyczne niekorzystnie wpłynąć na wydajność obciążenia. Utworzone przez automatyczne dostrajanie indeksów są niewidoczne dla operacji konserwacji na podstawowy schemat. Zmiany schematu, takie jak porzucenie lub zmienianie nazw kolumn nie są blokowane przez obecności Indeksy tworzone automatycznie. Indeksów, które są automatycznie tworzone przez usługę Azure SQL Database są usuwane natychmiast, kiedy związane z tabeli lub kolumny jest porzucany.

## <a name="automatic-plan-choice-correction"></a>Planowanie automatycznego wyboru korekty

Automatyczne plan korekty jest nową funkcją automatycznego dostrajania dodany do programu SQL Server 2017 CTP2.0 identyfikujący planów SQL, które błędne działanie. Opcja automatycznego dostrajania będzie wkrótce dostępne w bazie danych SQL Azure. Aby uzyskać więcej informacji o [automatycznego dostrajania w programu SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Następne kroki

- Aby włączyć automatyczne dostrajanie w bazie danych SQL Azure i umożliwić funkcji automatycznego dostrajania obciążenie w pełni zarządzać, zobacz [Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md).
- Umożliwia ręczne dostrajania, możesz przejrzeć [dostrajanie zalecenia w portalu Azure](sql-database-advisor-portal.md) i ręcznie zastosować te, które poprawić wydajność kwerend.
