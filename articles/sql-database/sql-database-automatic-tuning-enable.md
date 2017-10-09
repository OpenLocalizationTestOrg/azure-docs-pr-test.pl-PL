---
title: "aaaEnable automatycznego dostrajania dla usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Można włączyć automatycznego dostrajania bazy danych SQL Azure łatwe."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Włączanie automatycznego dostrajania

Baza danych SQL Azure jest usługą automatycznie zarządzanych danych, która stale monitoruje zapytań i identyfikuje akcji hello wykonanie tooimprove wydajność obciążenia. Możesz przejrzeć zalecenia i ręcznie zastosować je lub pozwól bazy danych SQL Azure automatyczne stosowanie działania naprawcze — jest to nazywane **automatycznego dostrajania tryb**. Dostrajanie automatycznego można włączyć na poziomie bazy danych hello lub powitania serwera.

## <a name="enable-automatic-tuning-on-server"></a>Włączanie automatycznego dostrajania na serwerze

tooenable automatycznego dostrajania na serwerze bazy danych SQL Azure, przejdź toohello server na platformie Azure w portalu, a następnie wybierz opcję **automatycznego dostrajania** hello menu. Wybierz hello automatycznego dostrajania opcje tooenable a wybierz **Zastosuj**:

![Serwer](./media/sql-database-automatic-tuning-enable/server.png)

Automatycznego dostrajania opcji na serwerze są baz danych tooall zastosowane na powitania serwera. Domyślnie wszystkie bazy danych odziedziczyć konfiguracji hello z ich nadrzędnego serwera, ale to zastąpione i określić osobno dla każdej bazy danych.

## <a name="configure-automatic-tuning-on-database"></a>Konfigurowanie automatycznego dostrajania dla bazy danych

Hello Azure umożliwia portalu tooindividually możesz określić hello automatycznego dostrajania konfiguracji w każdej bazie danych.

> [!NOTE]
> Ogólne zalecenie Hello jest toomanage hello automatycznego dostrajania konfiguracji na poziomie serwera tak hello tych samych ustawień konfiguracji mogą być automatycznie stosowane w każdej bazie danych. Konfigurowanie automatycznego dostrajania dla poszczególnych bazy danych, gdy hello bazy danych jest inny, że hello inne, na tym samym serwerze.
>

bazy danych toohello w hello portalu Azure Przejdź tooenable automatycznego dostrajania dla jednej bazy danych, a następnie i wybierz **automatycznego dostrajania**. Można skonfigurować ustawienia hello tooinherit pojedynczej bazy danych z bazy danych hello zaznaczając pole wyboru hello lub hello konfiguracji bazy danych można określić osobno.

![Database (Baza danych)](./media/sql-database-automatic-tuning-enable/database.png)

Po wybraniu odpowiedniej konfiguracji, kliknij przycisk **Zastosuj**.

## <a name="next-steps"></a>Następne kroki
* Witaj odczytu [automatycznego dostrajania artykułu](sql-database-automatic-tuning.md) toolearn więcej informacji na temat automatycznego dostrajania i jak go w celu poprawy wydajności.
* Zobacz [zaleceń](sql-database-advisor.md) omówienie zaleceń wydajności bazy danych SQL Azure.
* Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) toolearn o wyświetlaniu hello wpływ na wydajność kwerend top.
