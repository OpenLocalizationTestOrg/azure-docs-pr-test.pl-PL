---
title: "PowerShell przykład importowania pliku BACPAC pliku usługa Azure SQL database | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell do importowania pliku pliku BACPAC do bazy danych SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data, mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c24a3b7551058a69cbfdddf8b859b635e0829402
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/07/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a>Importowanie pliku pliku BACPAC bazy danych Azure SQL przy użyciu programu PowerShell

Ten przykładowy skrypt programu PowerShell importuje bazy danych z pliku BACPAC pliku do bazy danych Azure SQL.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowy skrypt następującego polecenia można usunąć grupy zasobów i wszystkie zasoby skojarzone z nim.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Tworzy serwer logiczny, który jest hostem bazy danych SQL. |
| [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | Tworzy regułę zapory zezwalają na dostęp do wszystkich baz danych na serwerze z wprowadzony zakres adresów IP. |
| [Nowe AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | Importy pliku BACPAC plików i utworzyć nową bazę danych na serwerze. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady skryptów programu PowerShell bazy danych SQL można znaleźć w [skryptów programu PowerShell bazy danych SQL Azure](../sql-database-powershell-samples.md).
