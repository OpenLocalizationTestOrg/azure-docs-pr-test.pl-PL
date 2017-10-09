---
title: "Narzędzie zadania elastycznej bazy danych toouninstall aaaHow"
description: "Jak toouninstall hello narzędzia zadania elastycznej bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Odinstaluj składniki zadania elastycznej bazy danych
**Zadania elastyczne bazy danych** składniki można odinstalować za pomocą portalu hello lub programu PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Odinstaluj składniki zadania elastycznej bazy danych przy użyciu hello portalu Azure
1. Otwórz hello [portalu Azure](https://portal.azure.com/).
2. Przejdź toohello subskrypcji, która zawiera **zadania elastycznej bazy danych** składniki, to znaczy hello subskrypcji, w których elastycznej bazy danych zostały zainstalowane składniki zadania.
3. Kliknij przycisk **Przeglądaj** i kliknij przycisk **grup zasobów**.
4. Witaj wybierz grupę zasobów o nazwie "__ElasticDatabaseJob".
5. Usuń grupę zasobów hello.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Odinstaluj składniki zadania elastycznej bazy danych przy użyciu programu PowerShell
1. Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź toohello narzędzia podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: typ **narzędzia cd**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > Narzędzia dysku cd
2. Uruchom skrypt programu PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > C:.\UninstallElasticDatabaseJobs.ps1 PS odblokowanie pliku\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >. \ UninstallElasticDatabaseJobs.ps1

Lub po prostu wykonać hello następującego skryptu, przy założeniu, domyślne wartości w przypadku na instalację składników hello:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Następne kroki
Zainstaluj toore zadania elastycznej bazy danych, zobacz [instalowania usługi zadania elastycznej bazy danych hello](sql-database-elastic-jobs-service-installation.md)

Omówienie zadania elastycznej bazy danych, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).

<!--Image references-->


