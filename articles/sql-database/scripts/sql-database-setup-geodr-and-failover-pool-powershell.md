---
title: "PowerShell aktywny przykład puli replikację geograficzną usługa Azure SQL database | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do konfigurowania aktywna replikacja geograficzna puli bazy danych Azure SQL"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a>Aby skonfigurować aktywna replikacja geograficzna puli bazy danych Azure SQL za pomocą programu PowerShell

Ten przykładowy skrypt programu PowerShell konfiguruje aktywna replikacja geograficzna dla bazy danych Azure SQL w puli elastycznej i awaryjnie do repliki pomocniczej bazy danych Azure SQL.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a>Przykładowe skrypty

[!code-powershell[główne](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Konfigurowanie aktywna replikacja geograficzna dla puli elastycznej")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Tworzy serwer logiczny, który jest hostem bazy danych lub elastyczna pula. |
| [Nowe AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | Tworzy elastycznej puli w ramach serwera logicznego. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Tworzy bazę danych w serwera logicznego jako jedną lub puli bazy danych. |
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | Aktualizuje właściwości bazy danych lub bazy danych są przenoszone do z i między pule elastyczne. |
| [Nowe AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych. |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)| Pobiera jeden lub więcej baz danych. |
| [Zestaw AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| Zmienia pomocniczej bazy danych jako głównej w celu zainicjowania trybu failover.|
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | Pobiera linki — replikacja geograficzna między bazą danych SQL Azure i grupy zasobów lub SQL Server. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |
|||

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).
