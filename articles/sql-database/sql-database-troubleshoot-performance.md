---
title: "aaaMonitoring & dostrajanie wydajności — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Porady dotyczące dostrajania w bazie danych SQL Azure za pośrednictwem oceny i poprawa wydajności."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "dostrajanie wydajności bazy danych dostrajanie dostrajanie wskazówki dotyczące wydajności programu sql wydajności programu SQL dostrajania wydajności bazy danych sql"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>Monitorowanie i dostrajanie wydajności

Azure SQL Database odbywa się automatycznie i usługa elastyczne danych, gdzie można łatwo monitorować użycie, dodawane lub usuwane zasobów (Procesora, pamięci, we/wy), Znajdź zaleceń, które mogą poprawić wydajność bazy danych lub umożliwić dostosowanie tooyour obciążenie bazy danych i automatycznie optymalizacji wydajności.

Ten artykuł zawiera omówienie monitorowania i opcje, które są dostępne w bazie danych SQL Azure dostrajania wydajności.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>Monitorowanie i rozwiązywanie problemów z wydajnością bazy danych

Azure umożliwia bazy danych SQL tooeasily możesz monitorować użycie bazy danych i identyfikacji zapytania, które mogą powodować problemy z wydajnością hello. Można monitorować wydajność bazy danych przy użyciu usługi Azure widoków portalu lub systemu. Dostępne są następujące opcje monitorowania i rozwiązywania problemów z wydajnością bazy danych hello:

1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **baz danych**, wybierz hello bazę danych, a następnie użyj hello monitorowanie wykresu toolook zasobów zbliża się ich maksymalna. Użycie jednostek DTU jest wyświetlane domyślnie. Kliknij przycisk **Edytuj** toochange hello przedział czasu i wartości wyświetlane.
2. Użyj [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) tooidentify hello zapytań, które spędzają tekst hello najbardziej zasobów.
3. Można użyć dynamicznych widoków zarządzania (widoków DMV), zdarzeń rozszerzonych (`XEvents`), a hello magazyn zapytań w programie SSMS parametrów wydajności tooget w czasie rzeczywistym.

Zobacz hello [tematu wskazówki dotyczące wydajności](sql-database-performance-guidance.md) techniki toofind można użyć tooimprove wydajności bazy danych SQL Azure po zidentyfikowaniu niektórych problem przy użyciu tych raportów lub widoków.

> [!IMPORTANT] 
> Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Optymalizacja wydajności tooimprove bazy danych

Baza danych SQL Azure pozwala tooimprove możliwości tooidentify oraz zoptymalizować wydajność zapytań bez zmieniania zasobów, przeglądając [zalecenia dotyczące dostrajania wydajności](sql-database-advisor.md). Częstymi przyczynami słabej wydajności bazy danych są brakujące indeksy i nieprawidłowo zoptymalizowane zapytania. Można stosować te zalecenia dotyczące dostrajania wydajności tooimprove obciążenia.
Możesz również bazy danych Azure SQL umożliwiają zbyt[automatycznie zoptymalizować wydajność kwerend](sql-database-automatic-tuning.md) , stosując wszystkie zidentyfikowane zalecenia i sprawdzanie, czy poprawiają wydajność bazy danych. Program hello następujące opcje tooimprove wydajność bazy danych:

1. Użyj [doradcy bazy danych SQL](sql-database-advisor-portal.md) tooview zalecenia dotyczące tworzenia i usuwanie indeksów, parametryzacja zapytań i rozwiązywania problemów ze schematu.
2. [Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md) i pozwól Azure SQL bazy danych automatycznie poprawka zidentyfikowane problemy z wydajnością.

## <a name="improving-database-performance-with-more-resources"></a>Poprawa wydajności bazy danych przy użyciu więcej zasobów

Ponadto nie ma żadnych towarów działań, które może poprawić wydajność bazy danych, można zmienić hello ilość zasobów dostępnych w bazie danych SQL Azure. Można przypisać więcej zasobów, zmieniając hello [warstwy usług](sql-database-service-tiers.md) autonomicznej bazy danych lub zwiększyć hello Edtu elastycznej puli w dowolnym momencie.
1. W przypadku autonomicznej bazy danych, możesz [zmiana warstw usług](sql-database-service-tiers.md) tooimprove na żądanie wydajność bazy danych.
2. W przypadku wielu baz danych, rozważ zastosowanie [pule elastyczne](sql-database-elastic-pool-guidance.md) zasobów tooscale automatycznie.

## <a name="tune-and-refactor-application-or-database-code"></a>Dostrajanie i zrefaktoryzuj aplikacji lub kodu bazy danych

Toomore kodu aplikacji można zmienić optymalnie Użyj hello bazy danych, zmień indeksów, wymusić planów lub użyj wskazówek toomanually dostosowanie hello bazy danych tooyour obciążenia. Znajdź pewne wskazówki i porady ręczne dostosowywania i poprawiania kodu hello w hello [tematu wskazówki dotyczące wydajności](sql-database-performance-guidance.md) artykułu.


## <a name="next-steps"></a>Następne kroki

- tooenable automatycznego dostrajania w bazie danych SQL Azure i umożliwiają automatyczne dostrajania funkcji w pełni zarządzać obciążenie, zobacz [Włączanie automatycznego dostrajania](sql-database-automatic-tuning-enable.md).
- toouse ręczne dostrajanie możesz przejrzeć [dostrajanie zalecenia w portalu Azure](sql-database-advisor-portal.md) i ręcznie zastosować hello te, które poprawić wydajność kwerend.
- Zmień zasoby, które są dostępne w bazie danych, zmieniając [warstwach usług bazy danych SQL Azure](sql-database-performance-guidance.md)