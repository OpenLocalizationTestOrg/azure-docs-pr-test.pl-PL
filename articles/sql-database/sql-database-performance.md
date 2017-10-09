---
title: "aaaMonitor i zwiększyć wydajność — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Azure SQL Database zapewnia wydajność powitalne narzędzi toohelp identyfikacji obszarów, które może poprawić wydajność kwerend bieżącej."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a>Monitorowanie i poprawianie wydajności
Baza danych SQL Azure identyfikuje potencjalne problemy w bazie danych i zalecane akcje, które może poprawić wydajność obciążenia przez podanie inteligentnego akcje dostosowywania i zalecenia.

tooreview Twojego wydajność bazy danych, użyj hello **wydajności** kafelka na stronie Przegląd hello lub zbyt przechodzenia "Obsługa + Rozwiązywanie problemów" sekcji:

   ![Widok wydajności](./media/sql-database-performance/entries.png)

W sekcji hello "Obsługa + Rozwiązywanie problemów" można użyć hello następujące strony:


1. [Omówienie wydajności](#performance-overview) toomonitor wydajność bazy danych. 
2. [Zalecenia dotyczące wydajności](#performance-recommendations) toofind zalecenia dotyczące wydajności, które może poprawić wydajność obciążenia.
3. [Szczegółowe informacje o wydajności zapytań](#query-performance-insight) toofind zasobu najwyższego korzystanie z zapytania.
4. [Automatycznego dostrajania](#automatic-tuning) toolet bazy danych SQL Azure automatycznie zoptymalizować bazę danych.

## <a name="performance-overview"></a>Wydajności — omówienie
Ten widok zawiera podsumowanie wydajność bazy danych i pomaga wydajności dostrajanie i rozwiązywania problemów. 

![Wydajność](./media/sql-database-performance/performance.png)

* Witaj **zalecenia** Kafelek zawiera podział dostrajanie zalecenia dotyczące bazy danych (trzy najważniejsze zalecenia są wyświetlane czy więcej). Kliknięcie tego kafelka przejście zbyt**[zaleceń](#performance-recommendations)**. 
* Witaj **dostrajanie działania** kafelka zawiera podsumowanie hello bieżących i zakończonych, dostrajanie akcji dla bazy danych, umożliwiając zapewnia szybki wgląd w historię hello dostrajanie działania. Kliknięcie tego kafelka przyjmuje toohello pełne, dostrajanie widoku Historia dla bazy danych.
* Witaj **autostrojenie** kafelka zawiera hello [automatycznego dostrajania konfiguracji](sql-database-automatic-tuning-enable.md) bazy danych (dostrajanie opcje, które są automatycznie stosowane tooyour bazy danych). Kliknięcie tego kafelka otwiera okno dialogowe konfiguracji automatyzacji hello.
* Witaj **zapytań bazy danych** kafelka przedstawia hello podsumowanie hello wydajność zapytań dla bazy danych (ogólną jednostek dtu w warstwie użycia i od góry zasobów korzystających z kwerendy). Kliknięcie tego kafelka przejście zbyt**[szczegółowe informacje o wydajności zapytań](#query-performance-insight)**.

## <a name="performance-recommendations"></a>Zalecenia dotyczące wydajności
Ta strona zawiera inteligentnego [dostrajanie zalecenia](sql-database-advisor.md) które może poprawić wydajność bazy danych. następujące typy zalecenia Hello są wyświetlane na tej stronie:

* Zalecenia, na które toocreate indeksy lub Usuń.
* Zalecenia dotyczące problemów schematu są identyfikowane w hello bazy danych.
* Zalecenia dotyczące zapytań mogą korzystać z zapytania parametrycznego.

![Wydajność](./media/sql-database-performance/recommendations.png)

Można również znaleźć dostrajanie akcje, które zostały zastosowane w przeszłości hello pełnej historii.

Dowiedz się, jak toofind Zastosuj zalecenia dotyczące wydajności w [Znajdowanie i stosować zalecenia wydajności](sql-database-advisor-portal.md) artykułu.

## <a name="automatic-tuning"></a>Automatyczne dostrajanie
Bazy danych SQL Azure mogą automatycznie dostrajania wydajności bazy danych poprzez zastosowanie [zaleceń](sql-database-advisor.md). toolearn, przeczytaj [automatycznego dostrajania artykułu](sql-database-automatic-tuning.md). tooenable, przeczytaj [sposób automatycznego dostrajania tooenable](sql-database-automatic-tuning-enable.md).

## <a name="query-performance-insight"></a>Szczegółowe informacje o wydajności zapytań
[Szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) pozwala toospend mniej czasu Rozwiązywanie problemów z wydajnością bazy danych przez zapewnienie:

* Bardziej szczegółowe informacje na temat użycia zasobów (bazy danych DTU) bazy danych. 
* Korzystanie z zapytań, które potencjalnie dostrajania dla procesora CPU top Hello wyższą wydajność. 
* Witaj toodrill możliwości w dół do szczegółów hello zapytania. 

  ![pulpit nawigacyjny wydajności](./media/sql-database-query-performance/performance.png)

Więcej informacji dotyczących tej strony można znaleźć w artykule hello  **[jak toouse szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md)**.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Azure wytyczne dotyczące wydajności bazy danych SQL dla pojedynczych baz danych](sql-database-performance-guidance.md)
* [Kiedy należy użyć puli elastycznej?](sql-database-elastic-pool-guidance.md)

