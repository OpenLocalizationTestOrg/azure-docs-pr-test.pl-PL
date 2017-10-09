---
title: "Przykłady skryptów PowerShell aaaAzure bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure PowerShell skryptu przykłady toohelp możesz utworzyć i zarządzać nimi bazy danych SQL Azure serwerów, elastyczne pule baz danych i zapory."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Przykładów dla platformy Azure PowerShell bazy danych SQL Azure

Witaj Poniższa tabela zawiera linki toosample programu Azure PowerShell skryptów bazy danych SQL Azure.

| |  |
|---|---|
|**Utworzyć pojedynczą bazę danych i elastycznej puli**||
| [Utworzyć pojedynczą bazę danych i skonfigurować reguły zapory](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell tworzy pojedynczej bazy danych Azure SQL i konfiguruje regułę zapory poziomu serwera. |
| [Tworzenie elastycznych pul i przeniesienie puli baz danych](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell tworzy pule elastyczne bazy danych SQL Azure i przenosi puli baz danych, a następnie zmienia poziomy wydajności.|
|**Konfigurowanie replikacji geograficznej i trybu failover**||
| [Konfigurowanie i pracy awaryjnej pojedynczej bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla pojedynczej bazy danych Azure SQL i awaryjnie toohello repliki pomocniczej. |
| [Konfigurowanie i pracy awaryjnej puli bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla bazy danych Azure SQL w puli elastycznej SQL, a nie powiedzie się za pośrednictwem toohello repliki pomocniczej. |
| [Konfigurowanie i trybu failover, a praca awaryjna grupy dla pojedynczej bazy danych (wersja zapoznawcza)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell konfiguruje grupę pracy awaryjnej dla wystąpienia serwera bazy danych SQL Azure dodaje grupę trybu failover toohello bazy danych, a nie powiedzie się za pośrednictwem serwera pomocniczego toohello |
|**Skalowania pojedynczej bazy danych i elastycznej puli**||
| [Skalowania pojedynczej bazy danych](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell monitoruje hello metryki wydajności bazy danych Azure SQL, skaluje go tooa wyższy poziom wydajności i tworzy regułę alertu w jednym z hello metryki wydajności. |
| [Skala puli elastycznej](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell monitoruje hello metryk wydajności puli elastycznej bazy danych SQL Azure, skaluje go tooa wyższy poziom wydajności i tworzy regułę alertu w jednym z hello metryki wydajności.  |
| **Inspekcja i wykrywania zagrożeń** |
| [Konfigurowanie inspekcji i wykrywanie zagrożeń](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell konfiguruje zasady wykrywania inspekcji i zagrożeń dla bazy danych Azure SQL. |
| **Przywracanie, kopiowanie i Importowanie bazy danych**||
| [Przywracanie bazy danych](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell przywraca bazę danych Azure SQL z geograficznie nadmiarowej kopii zapasowej i przywrócenie usuniętych Azure SQL toohello najnowszej kopii zapasowej bazy danych. |
| [Skopiuj toonew serwer bazy danych](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell tworzy kopię istniejącej bazy danych Azure SQL w nowy serwer Azure SQL. |
| [Importuj z pliku pliku bacpac bazy danych](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ten skrypt programu PowerShell importuje serwer bazy danych Azure SQL tooan z pliku pliku bacpac. |
| **Synchronizowanie danych między bazami danych**||
| [Synchronizowanie danych między bazami danych SQL](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell konfiguruje toosync synchronizacji danych między wiele baz danych Azure SQL. |
| [Synchronizowanie danych między bazy danych SQL i programu SQL Server lokalne](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ten skrypt programu PowerShell konfiguruje toosync synchronizacji danych między bazą danych Azure SQL i lokalnej bazy danych programu SQL Server. |
|||
|||
