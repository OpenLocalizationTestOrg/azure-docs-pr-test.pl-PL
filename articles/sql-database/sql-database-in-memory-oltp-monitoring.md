---
title: "Magazyn w pamięci XTP aaaMonitor | Dokumentacja firmy Microsoft"
description: "Szacowana i monitorowanie magazynu w pamięci XTP korzystać, pojemności; Napraw błąd pojemności 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Monitorowanie magazynu OLTP w pamięci
Korzystając z [OLTP w pamięci](sql-database-in-memory.md), dane w tabelach zoptymalizowanych pod kątem pamięci i zmiennych tabel znajdują się w magazynie OLTP w pamięci. Każda warstwa usług Premium ma maksymalny rozmiar magazynu OLTP w pamięci, które opisano w hello [artykułu warstwach usług bazy danych SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Po przekroczeniu tego limitu insert i zaktualizować operacji mogą kończyć się niepowodzeniem (z powodu błędu 41823). W tym momencie zostanie potrzebują tooeither usuwania danych tooreclaim pamięci lub Uaktualnij warstwę wydajności hello bazy danych.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Określić, czy dane będą pasować hello zakończenia przechowywania w pamięci
Określić limit magazynu hello: Zapoznaj się hello [artykułu warstwach usług bazy danych SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) dla caps magazynu hello hello różnych poziomów usług Premium.

Szacowanie pamięci wymagania dla tabeli zoptymalizowanej pod kątem pamięci działa hello sam sposób dla programu SQL Server, ponieważ jest w bazie danych SQL Azure. Potrwać kilka minut tooreview tematu [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Należy pamiętać, że tabela hello i zmiennej wiersze tabeli, a także indeksów, są wliczane do rozmiaru danych przez użytkownika maksymalną hello. Ponadto instrukcji ALTER TABLE musi mieć wystarczającej ilości miejsca toocreate nowej wersji hello całą tabelę i jego indeksy.

## <a name="monitoring-and-alerting"></a>Monitorowanie i zgłaszanie alertów
Można monitorować użycie magazynu w pamięci w procentach hello [cap magazynu dla warstwę wydajności](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) w hello Azure [portal](https://portal.azure.com/): 

* W bloku bazy danych hello Znajdź okno wykorzystania zasobów hello, a następnie kliknij przycisk Edytuj.
* Następnie wybierz metrykę hello `In-Memory OLTP Storage percentage`.
* tooadd alert, kliknij na powitania wykorzystania zasobów pole tooopen hello metryki bloku, a następnie kliknij pozycję Dodaj alert.

Lub użyj hello następujące zapytanie hello tooshow wartość użycia magazynu w pamięci:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Popraw sytuacji braku pamięci — błąd 41823
W operacji INSERT, UPDATE i Utwórz się niepowodzeniem z komunikatem o błędzie 41823 uruchomione wyniki braku pamięci.

Komunikat o błędzie 41823 wskazuje, że hello tabel zoptymalizowanych pod kątem pamięci i zmiennych tabel Przekroczono maksymalny rozmiar hello.

tooresolve ten błąd, albo:

* Usuwanie danych z tabel zoptymalizowanych pod kątem pamięci hello, potencjalnie Odciążanie tootraditional danych hello, tabel opartej na dysku. lub,
* Uaktualnij tooone warstwy usługi hello za mało przechowywania w pamięci dla danych hello należy tookeep w tabelach zoptymalizowanych pod kątem pamięci.

## <a name="next-steps"></a>Następne kroki
Do monitorowania wskazówki, zobacz [monitorowania bazy danych SQL Azure przy użyciu dynamicznych widoków zarządzania](sql-database-monitoring-with-dmvs.md).
